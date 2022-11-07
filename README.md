<h1>TryHackMe - Surfer</h1>
<img src="./img/logo.png" alt="logo" width="400">
<ul>
    <li>
        <strong>Step 1 :</strong> Rustscan<br>
        <ul>
            <code>10.10.51.39:22</code> SSH<br>
            <code>10.10.51.39:80</code> http
        </ul>
    </li><br>
    <li>
        <strong>Step 2 :</strong> Checking WebApplication (because bruteforcing ssh won't get us anywhere).
        <ul>
            <img src="./img/WebApplication.png" alt="WebApplication" height="300">
        </ul>
    </li><br>
    <li>
        <strong>Step 3 :</strong> Brute forcing login page.<br>
        <ul>
            Trying out some default credentials.<br>
            <img src="./img/loggedIn.png" alt="loggedIn" height="300"><br>
            One of them worked.
        </ul>
    </li><br>
    <li>
        <strong>Step 4 :</strong> Back to reconnaissance.<br>
        <ul>
            <li>Export to pdf looks intresting.</li>
            <li>Searching google for <strong>export to pdf</strong> vulnerability.</li>
            <li>Searching that led me to <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a> medium post by <strong>Inon Shkedy.</strong></li>
        </ul>
    </li><br>
    <h2>Following his lead.</h2>
    <li>
        <strong>Step 5 :</strong> Monitoring the request.
        <ul>
            <img src="./img/request.png" alt="request"><br>
            Looking at the <code>url</code> parameter we can say that <code>Internal Network Exposure(SSRF)</code> vulnerability. It also made me think i can read other files on that localhost. Maybe one of them containing credential for ssh, ssh private key or anything that can help me get a foothold.
        </ul>
    </li>
</ul>










<!-- <ol>
    <li>
        <h3>Port-Scanning:</h3>
        <img src="./img/rustscan.png" alt="rustscan" width="500"><br>
        Starting with <code>rustscan</code>. We can see that only two ports are open.<br>
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
        I was going through the page and found this option. If there was anything on this page <br>
        that could help me, was this option. So, i searched <code>Export pdf vulnerability</code> and <br>
        found <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a>. This is a medium post by <strong>Inon Shkedy</strong> where he explains <code>Export Injection</code>.
        <br>The first step was to capture and monitor the http request.
    </li><br>
    <li>
        <h3>HTTP request:</h3>
        <img src="./img/req.png" alt="req-1" width="450"> <img src="./img/reqParam.png" alt="reqParam" width="250"><br>
        I intercepted the request using <code>burpsuite</code> and url-decoded the <code>url</code> parameter. We <br>
        can see that it has <code>Internal Network Exposure(SSRF)</code> vulnerability. I thought of <br>
        internal port scanning like the post from <strong>Inon</strong> suggested but i don't know how to do <br>
        it so i had another idea. I wanted to bruteforce and see if there are any other pages like <br>
        <code>server-info.php</code> that we could access on that internal network. I tried some basic ones <br>
        but they weren't helpful. So, let's use ffuf and try to find other files.
    </li><br>
    <li>
        <h3>FFUF:</h3>
        <img src="./img/ffuf.png" alt="ffuf" width="600"><br>
        I grabbed <code>Content-Type</code> and <code>Cookie</code> from the burpsuite request header we intercepted <br>
        and used them in ffuf command which you can see in the image. You might have noticed that <br>
        my machine ip has changed and that's because my 1 hour was over and i forgot to extend it.<br>
        So, i found some files and folders. This machine has <code>port 22</code> open and since it is <br>
        a CTF, my next move is to find any file which might contain the login credentials for SSH.<br>
        I will check out all the files and use ffuf on the folders again.
    </li><br>
    <li>
        <h3>Flag:</h3>
        <img src="./img/flag.png" alt="flag" width="500"><br>
        Instead of finding the login credentials for SSH, i found the flag. I can't include the files <br>
        location because i want this writeup to be accepted. All i can say is that i found an <br>
        intresting file inside a folder. i then used that files location in the <code>url</code> parameter <br>
        by intercepting the request in burp and forwarded it. The file i received back as pdf had the flag.
    </li>
</ol> -->
<!-- <p>Machine Solved 😁</p> -->