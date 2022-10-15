<h1>TryHackMe - Surfer</h1>
<img src="./img/logo.png" alt="logo" width="400">
<p>I there were a lot of things that i tried but were not helpful and including them will only waste <br>your time so i will only include the steps that showed me any result</p>

<ol>
    <li>
        <h3>Port-Scanning:</h3>
        <img src="./img/rustscan.png" alt="rustscan" width="500"><br>
        Starting with rust scan we can see that only two ports are open.<br>
        Trying to brute force SSH is useless so lets checkout the webpage.
    </li><br>
    <li>
        <h3>WebPage:</h3>
        <img src="./img/web-page.png" alt="web-page" width="500"><br>
        Were land on this login.php page.<br>
        Let's try some default credentials before using sqlmap or hydra.<br>
    </li><br>
    <li>
        <h3>LogIn Page:</h3>
        <img src="./img/index-page.png" alt="login-page" width="500"><br>
        One of those default credentials worked and now we are logged in.
    </li><br>
    <li>
        <h3>Index Page:</h3>
        <img src="./img/export.png" alt="export" width="500"><br>
        I was going through the page and found this. if there was anything on this page that could halp me was this option.<br>
        So i search "Export pdf vulnerability" and found <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a>.<br>
        The first step was to capture and monitor the http request.
    </li><br>
    <li>
        <h3>HTTP request:</h3>
        <img src="./img/req-1.png" alt="req-1" width="450"> <img src="./img/req-1param.png" alt="req-1param" width="280"><br>
        I intercepted the request using burp and url-decoded the <code>url</code> parameter.<br>
        So, we can see that it has Internal Network Exposure(SSRF) vulnerability.<br>
        I thought of internal port scanning like the post from Inon suggested but i don't know how to do it so i had another idea.<br>
        I wanted to bruteforce and see if there are any other pages like <code>server-info.php</code> that we could access on that internal network.<br>
        I tried some basic ones but it didn't help so lets use ffuf and see what we get.
    </li><br>
    <li>
        <h3>FFUF:</h3>
        <img src="./img/ffuf-1.png" alt="ffuf-1" width="600"><br>
        I grabbed all the important stuff from the burp request and used them in ffuf command and i found these files and folders.<br>
        This machine has <code>port 22</code> and since it is a CTF, my next move is to find any file which might contain the login credentials for SSH.<br>
        I will ffuf all the folders for intresting files.
    </li><br>
    <li>
        Flag:<br>
        <img src="./img/flag.png" alt="flag" width="500"><br>
        Instead of finding the login credentials for SSH, i found the flag.<br>
        I can't include the files location because i want this writeup to be accepted so all i can say is that i found an intresting file inside a folder.<br>
        i then used that files location in the <code>url</code> parameter by intercepting the request in burp and forwarded it. The file i received as pdf had the flag.
    </li>
</ol>