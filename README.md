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
        Index Page:<br>
        <img src="./img/index-page.png" alt="index-page" width="500"><br>
        One of those default credentials worked and now we are logged in.
    </li><br>
    <li>
        Locating a vulnerability:<br>
        <img src="./img/export.png" alt="export" width="500"><br>
        I was going through the page and found this. if there was anything on this page that could halp me was this.<br>
        So i search "Export pdf vulnerability" and found <a href="https://inonst.medium.com/export-injection-2eebc4f17117">this</a>.<br>
        The first step was to capture and monitor the http request.
    </li>
</ol>