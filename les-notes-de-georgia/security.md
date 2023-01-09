# Security

Quelques petites règles basiques de sécurité en java

## SQL Injection

Password: ' or 1=1)#

The above resulted in the following SQL statement:
SELECT UserID FROM User
WHERE (email = 'alice@bank.com'
AND password = '' OR 1=1)#

Because this statement is both syntactically valid and OR 1=1 always returns true, the authentication mechanism is bypassed. Let us now analyze the vulnerability from the code perspective.

Prepared statements (aka parameterized queries) are the best mechanism for preventing SQL injection attacks.

Prepared statements are used to abstract SQL statement syntax from input parameters. Statement templates are first defined at the application layer, and the parameters are then passed to them.

Aside from a better protection against SQL injection attacks, prepared statements offer improved code quality from a legibility and maintainability perspective due to the separation of the SQL logic from its inputs.

Bad
//String sql = "select * from users where (email ='" + email +"' and password ='" + password + "')";
//ResultSet result = statement.executeQuery(sql);

Good
String sql = "select * from users where email = ? and password = ? ";
PreparedStatement preparedStatement = connection.prepareStatement(sql);
preparedStatement.setString(1, email);
preparedStatement.setString(2, password);
ResultSet result = preparedStatement.executeQuery();


## XXE Processing

In this interactive tutorial you will understand how XML eXternal Entity (XXE) processing attacks are used to compromise the security of a web application, and how to write code more securely to protect against this type of attack.

Note: Throughout this module we will use the following terms interchangeably: XML Parser, SAX Parser and XML Processor.

An XXE attack works by taking advantage of a feature in XML, namely XML eXternal Entities (XXE) that allows external XML resources to be loaded within an XML document.

By submitting an XML file that defines an external entity with a file:// URI, an attacker can effectively trick the application's SAX parser into reading the contents of arbitrary file(s) that reside on the server-side filesystem.

BAD

<!DOCTYPE foo [<!ELEMENT foo ANY >
<!ENTITY bar SYSTEM "file:///etc/passwd" >]>
<?xml version="1.0" encoding="UTF-8"?>
<trades>
<metadata>
<name>Apple Inc</name>
<stock>APPL</stock>
<trader>
<foo>&bar;</foo>
<name>C.K Frode</name>
</trader>
</metadata>
</trades>

Because of this vulnerability any file on the remote server (or more precisely, any file that the web server has read access to) could be obtained.

A malicious attacker could easily use this to gain access to arbitrary files such as system files, or files containing sensitive data such as passwords or user data.

To use these parsers safely, you have to explicitly disable referencing of external entities in the SAX parser implementation you use. We'll revisit this in the remediation section later.

DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
documentBuilderFactory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
documentBuilderFactory.setFeature("http://xml.org/sax/features/external-general-entities", false);
documentBuilderFactory.setFeature("http://xml.org/sax/features/external-parameter-entities", false); 

## Command Injection

In this interactive tutorial, you will learn how a Command Injection attack is used to compromise the security of a web application, and how to write code more securely to protect against this type of attacks.

on UNIX systems ;id is a command that returns the user id for the user that ran the command.

we make use of Java's Pattern.matches() method to run a regular expression search on myUiD variable, identifying non alphanumeric characters e.g. ; , < , > , " , ' , & .

Should any non alphanumeric characters be encountered, the if check will fail and return, thus preventing malicious control shell characters from being passed to the statlab program.



## Session Fixation

In this interactive tutorial we will demonstrate how Session Fixation attack is used to compromise the security of a web application, and how to write code more securely to protect against this type of attack.

request.getSession(true);


A combination of the following best practices could help to defend against Session Fixation attacks:

1. Ensure that only server-generated session values are accepted by the application.

2. Upon a successful login, invalidate the original session token, and re-issue a new session token.

3. Prevent the application from accepting session tokens via GET or POST requests and instead store session values within HTTP cookies only.

Let us see how a potential fix can be applied to our vulnerable example to remediate the session fixation vulnerability.

// Prevent Session Fixation (http://en.wikipedia.org/wiki/Session_fixation)
HttpSession session = request.getSession(false);
if (session != null) {
session.invalidate();
}


## Use Of Insufficiently Random Values

In this interactive tutorial we will demonstrate how Insufficiently Random Values used in session token generation can compromise the security of a web application, and how to write code more securely to protect against this type of attacks.

Note that the problem with generating weak random values is not specific to web session generation and as such, its security implications must be considered when designing any software component that may require a random number generator.

the developers have not considered using a random number generator to generate their session identifier values and naively relied on using System.currentTimeMillis() method to ensure session uniqueness. The currentTimeMillis() returns the current time in milliseconds which is then passed to a string encoding function encode()

Once encoded, the returned session identifier is used by TradeHUB's session management API which leads to weak session identifiers being assigned for end users.

The best way to remediate the Insufficiently Random Values vulnerability is to use an algorithm that is currently considered to be strong by experts in the field, and select well-tested implementations with the seeds of the adequate length.

In general, if a pseudo-random number generator is not advertised as being cryptographically secure, it should not be used in security-sensitive contexts.

Pseudo-random number generators can produce predictable numbers if the generator is known and the seed can be guessed. A 256-bit seed is a good starting point for producing a "random enough" number.

Let's see how the above recommendations can be applied to our vulnerable example to improve our session token generator.

SecureRandom rand = new SecureRandom();
byte bytes[] = new byte[20];
rand.nextBytes(bytes);
String cookie = new String(Hex.encodeHex(bytes));
return cookie;

## Reflected Xss

In this interactive tutorial, we will demonstrate how Reflected Cross-Site Scripting (XSS) attacks can compromise the security of a web application, and how to write code more securely to protect against this type of attacks.
Reflected XSS is also known as Non-Persistent XSS, so we will use these terms interchangeably.

Using a stolen session token to access an application as another user is known as Session Hijacking.

This ability to execute a malicious script in a user's browser is known as a Cross-site Scripting vulnerability.

<c:when test="${f:h(allRecordCount) != 0}">
6
<jsp:include page="searchResults.jsp"/>
7
</c:when>
8
<c:otherwise>
9
<h4>No results found for: </h4>
10
  <p><em><strong><%= request.getParameter("search") %></strong></em></p>
11
</c:otherwise>


The main Reflected XSS remediation strategy is to treat all the user input as a text, not as a code. This can be achieved by the following actions:

1. Escape user input using language-specific or framework-specific instruments, like templates or contextual escaping. Usually, these mechanisms are enabled by default, so make sure not to disable them.

2. Know all the locations where user input is used, and try to avoid returning unsanitized user input to potentially dangerous locations like HTML body and attributes, javascript, GET parameters, URLs, links, CSS.

3. Use additional security controls that help to prevent XSS in case escaping controls fail or are missing.

HTTPOnly cookie flag. This flag prevents Javascript from accessing the cookie content, thus protecting it from being stolen if Reflected XSS is present.
Content Security Policy HTTP Header. This header restricts sources of all the page's content, including javascript code, to the whitelist of sources, thus making XSS exploitation more hard to perform.
X-XSS-Protection HTTP Header. This header prevents browsers from loading a page if they detect Reflected XSS exploitation.
Let's see how these techniques can be applied to our vulnerable example to remediate the Reflected XSS vulnerability.

The most effective method to protect against XSS attacks is by using JSTL's c:out tag or fn:escapeXml() EL function when displaying user-controlled input. These tags will automatically escape and encode HTML characters within the rendered HTML including < , > , " , ' and & thereby preventing injection of potentially malicious HTML code.

 <p><em><strong><c:out value="${<%= request.getParameter("search") %>}"/></strong></em></p>


## Stored (Persistent) Xss

In this interactive tutorial we will demonstrate how Stored Cross-Site Scripting (XSS) attacks can compromise the security of a web application, and how to write code more securely to protect against this type of attacks.

Stored XSS is also known as Persistent XSS, so we will use these terms interchangeably.


To defend against Stored Cross-Site Scripting attacks, it is important to ensure that user-supplied data output is encoded before being served by the application to other users.

Output encoding effectively works by escaping user-supplied data immediately before it is served to users of the application.

When the data is correctly escaped before being served to the user for display in their browser, the browser does not interpret it as code and instead interprets it as data, thus ensuring it does not get executed.

For example, the string <script> is converted to &lt;script&gt; when properly escaped and is simply rendered as text in the user's browser window rather than being interpreted as code.

Let's see how these techniques can be applied to our vulnerable example to remediate the Stored XSS vulnerability.

The most effective method to protect against XSS attacks is by using JSTL's c:out tag or fn:escapeXml() EL function when displaying user-controlled input. These tags will automatically escape and encode HTML characters within the rendered HTML including < , > , " , ' and & thereby preventing injection of potentially malicious HTML code.


## DOM Cross Site Scripting

In this interactive tutorial we will demonstrate how DOM-based XSS attacks can compromise the security of a web application, and how to write code more securely to protect against this type of attacks.

To defend against Cross-Site Scripting attacks in a Document Object Model (DOM) environment, a defense-in-depth approach is required, combining several security best practices.

You should recall that Stored XSS and Reflected XSS injections take place server-side rather than client-side. With DOM XSS, the attack is injected into the browser’s DOM thus adding complexity by making it very difficult to prevent and highly context specific (because an attacker can inject HTML, HTML Attributes, or CSS as well as URLs).

As a general set of principles, the application should first HTML-encode and then JavaScript-encode any user-supplied data that is returned to the client.

Due to the very broad attack surface, developers are strongly encouraged to review areas of code that are potentially susceptible to DOM XSS, including but not limited to:

window.name document.referrer document.URL document.documentURI location location.href location.search location.hash eval setTimeout setInterval document.write document.writeIn innerHTML outerHTML

Let us apply a suitable Regex pattern to remediate this DOM XSS vulnerability.


## Directory (Path) Traversal

In this interactive tutorial we will demonstrate how the Directory Traversal (also known as Path Traversal) attack can compromise the security of a web application, and how to write code more securely to protect against this type of attacks.

