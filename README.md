<h1>TryHackMe - Surfer</h1>
<img src="./img/logo.png" alt="logo" width="400">
<p>I there were a lot of things that i tried but were not helpful and including them will only waste your time so i will only include the steps that showed me any result</p>
<br>
<ol>
    <li>
        Port-Scanning:<br>
        <img src="./img/rustscan.png" alt="rustscan" width="500"><br>
        Starting with rust scan we can see that only two ports are open.<br>
        Trying to brute force SSH is useless so lets checkout the webpage.
    </li><br>
    <li>
        WebPage:<br>
        <img src="./img/web-page.png" alt="web-page" width="500"><br>
        Were land on this login.php page. Let's try some default credentials before using sqlmap or hydra.<br>
    </li><br>
    <li>
        LogIn Page:<br>
        <img src="./img/index-page.png" alt="login-page" width="500"><br>
        One of those default credentials worked and now we are logged in.
    </li><br>
    <li>
        Index Page:<br>
        <img src="./img/export.png" alt="export" width="500"><br>
        I was going through the page and found this. if there was anything on this page that could halp me was this option.<br>
        So i search "Export pdf vulnerability" and found <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a>.<br>
        The first step was to capture and monitor the http request.
    </li><br>
    <li>
        HTTP request:<br>
        <img src="./img/req-1.png" alt="req-1" width="400"><img src="./img/req-1param.png" alt="req-1param" width="300"><br>
        So, we can see that it has Internal Network Exposure(SSRF) vulnerability.<br>
        I thought of internal port scanning like the post from Inon suggested but i don't know how to do it so i had another idea.<br>
        I wanted to bruteforce and see if there are any other pages like <code>server-info.php</code> that we could access on that internal network.<br>
        I tried some basic ones but it didn't help so lets use ffuf and see what we get.
    </li>
</ol>