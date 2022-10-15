<h1>TryHackMe - Surfer</h1>
<img src="./img/logo.png" alt="logo" width="400">
<p>There were a lot of things that i tried but were not helpful and including them was only a waste <br>of time. So, i will only include the steps that showed me any result</p>

<ol>
    <li>
        <h3>Port-Scanning:</h3>
        <img src="./img/rustscan.png" alt="rustscan" width="500"><br>
        Starting with <code>rustscan</code> we can see that only two ports are open.<br>
        Trying to brute force SSH mostly fails. So, let's checkout the webpage first.
    </li><br>
    <li>
        <h3>WebPage:</h3>
        <img src="./img/web-page.png" alt="web-page" width="500"><br>
        We land on this <code>login.php</code> page.<br>
        Let's try some default credentials before using <code>sqlmap</code> or <code>hydra</code>.<br>
    </li><br>
    <li>
        <h3>LogIn Page:</h3>
        <img src="./img/index-page.png" alt="login-page" width="500"><br>
        One of those default credentials worked and now we are logged in.
    </li><br>
    <li>
        <h3>Index Page:</h3>
        <img src="./img/export.png" alt="export" width="500"><br>
        I was going through the page and found this. if there was anything on this page <br>
        that could help me, was this option. So, i search <code>Export pdf vulnerability</code> and <br>
        found <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a>. This is a medium post by <strong>Inon Shkedy</strong> where he explains <code>Export Injection</code>.
        <br>The first step was to capture and monitor the http request.
    </li><br>
    <li>
        <h3>HTTP request:</h3>
        <img src="./img/req.png" alt="req-1" width="450"> <img src="./img/reqParam.png" alt="reqParam" width="250"><br>
        I intercepted the request using <code>burpsuite</code> and url-decoded the <code>url</code> parameter. So, we can see that <br>it has Internal Network Exposure(SSRF) vulnerability.
        I thought of internal port scanning like the <br>post from Inon suggested but i don't know how to do it so i had another idea.
        I wanted to <br>bruteforce and see if there are any other pages like <code>server-info.php</code> that we could access on <br>that internal network.
        I tried some basic ones but it didn't help so lets use ffuf and see what we get.
    </li><br>
    <li>
        <h3>FFUF:</h3>
        <img src="./img/ffuf.png" alt="ffuf" width="600"><br>
        I grabbed all the important stuff from the burp request and used them in ffuf command and <br>i found these files and folders. This machine has <code>port 22</code> and since it is a CTF, my next move <br>is to find any file which might contain the login credentials for SSH.<br>
        I will ffuf all the folders for intresting files.
    </li><br>
    <li>
        <h3>Flag:</h3>
        <img src="./img/flag.png" alt="flag" width="500"><br>
        Instead of finding the login credentials for SSH, i found the flag. I can't include the files <br>location because i want this writeup to be accepted so all i can say is that i found an <br>intresting file inside a folder. i then used that files location in the <code>url</code> parameter by <br>intercepting the request in burp and forwarded it. The file i received as pdf had the flag.
    </li>
</ol>