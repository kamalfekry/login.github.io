
 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Sign In</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <link rel="stylesheet" href="./css/bootstrap.min.css">
    <style>
        body, html {
            margin: 0;
            padding: 0;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            background: url('./images/hayah-karima-banner-021710254873.png') no-repeat center center fixed ;
            
            background-size: cover;
        }
        .navbar {
            background-color: rgba(218, 225, 224, 0.5);
           
            padding: 10px 20px;
        }
        .navbar-brand {
            display: flex;
            align-items: center;
            font-weight: bold;
            font-size: 1.5rem;
        }
        .navbar-brand img {
            height: 70px;
            width: 140px;
            margin-right: 10px;
        }
        .navbar-nav .nav-link {
            color: #20a78b;
            font-weight: bold;
            margin-left: 10px;
        }
        .navbar-nav .nav-link:hover {
            color: #20a78b !important;
        }
        .container {
            max-width: 400px;
            margin: 100px auto 0 auto;
            padding: 20px;
            text-align: center;
            flex: 1;
        }
        .form-control {
            margin-bottom: 20px;
            
        }
        #captureButton {
            background-color: #ff7f00;
           border: none;
            color: white;
            padding: 10px 0;
        }
        #loginButton {
            background-color: #20a78b;
            border: none;
            color: white;
            padding: 10px 0;
        }
        #captureButton:hover, #loginButton:hover {
            opacity: 0.8;
        }
        .text-center {
            color: #20a78b;
            font-weight: bold;
        }
        #photoContainer {
            display: none;
            text-align: center;
        }
        #video {
            width: 100%;
            max-width: 320px;
            height: auto;
            border: 1px solid black;
        }
        .footer {
            background-color: #20a78b;
            color: white;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            position: sticky;
            bottom: 0;
            width: 100%;
        }
        .footer .social-icons {
            display: flex;
            justify-content: center;
            gap: 15px;
        }
        .footer .social-icons a {
            color: white;
            text-decoration: none;
            font-size: 1.2rem;
        }
        .footer .social-icons a:hover {
            color: #007bff;
        }
    </style>
</head>
<body>

<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-light fixed-top">
    <a class="navbar-brand" href="#">
        <img src="./images/logo.png" alt="Logo"> <!-- Replace with your actual logo path -->
    </a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ml-auto">
            <li class="nav-item">
                <a class="nav-link" href="signout.html">Sign Out</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" id="adminLink" href="admin.html">Admin Page</a>
            </li>
        </ul>
    </div>
</nav>


<div class="container">
    <h2 class="text-center mb-4">Employee Sign In</h2>
    <form id="loginForm">
        <div class="form-group">
            <input type="text" class="form-control" id="username" placeholder="Username :" required>
        </div>
        <button type="button" class="btn btn-block" id="captureButton">Capture a Photo</button>
        <button type="submit" class="btn btn-block mt-3" id="loginButton" disabled>Sign In</button>
    </form>
    <div id="photoContainer" class="mt-3">
        <video id="video" autoplay></video>
        <button type="button" class="btn btn-info mt-2" id="snapButton">Snap Photo</button>
        <canvas id="photoCanvas" width="320" height="240" class="mt-2"></canvas>
    </div>
</div>

<!-- Footer -->
<footer class="footer">
    <div>Hayat Kareema Foundation</div>
    <div class="social-icons">
        <a href="https://www.facebook.com/hayakarimaofficial" target="_blank"><i class="fab fa-facebook-f"></i></a>
        <a href="https://www.instagram.com/hayakarimaofficial/?hl=en" target="_blank"><i class="fab fa-instagram"></i></a>
        <a href="https://www.tiktok.com/@hayakarimatv" target="_blank"><i class="fab fa-tiktok"></i></a>
        <a href="https://www.linkedin.com/company/hayah-karima-foundation-%D9%85%D8%A4%D8%B3%D8%B3%D8%A9-%D8%AD%D9%8A%D8%A7%D8%A9-%D9%83%D8%B1%D9%8A%D9%85%D8%A9" target="_blank"><i class="fab fa-linkedin-in"></i></a>
        <a href="https://www.youtube.com/channel/UCOLOGmlnn-C_YFQMvOhm0Kg" target="_blank"><i class="fab fa-youtube"></i></a>
    </div>
    <div class="col-2" >
        <span id="element"></span>
    </div>
</footer>

<script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.2/dist/js/bootstrap.bundle.min.js"></script>
<script src="./js/bootstrap.bundle.min.js"></script>
<script src="./js/typed.js"></script>
<script src="https://unpkg.com/typed.js@2.1.0/dist/typed.umd.js"></script>
<script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('photoCanvas');
    const context = canvas.getContext('2d');
    const captureButton = document.getElementById('captureButton');
    const snapButton = document.getElementById('snapButton');
    const loginButton = document.getElementById('loginButton');
    const photoContainer = document.getElementById('photoContainer');
    const validUsernames = [
        "جني_السيد", "حسين_رشاد", "احمد_عبده", "اسراء_عبدالله", "دعاء_فاروق", 
        "شمس_محمد", "محمد_ابراهيم", "يوسف_عبدالحي", "هاجر_صلاح", "ياسر_يوسف",
        "محمد_سعيد", "اسراء_ياسين", "شادية_حسنين", "محمود_ابراهيم", "محمود_عبدالجيد",
        "منة_عبدالرحمن", "هيام_حلمي", "مريم_احمد", "يوسف_حسن", "نورهان_عبدالرحمن",
        "محمد_شكري", "فاطمة_محمد", "رنا_محمد", "مريم_يوسف", "رشا_محمد",
        "ندا_جلال", "نيرة_عبدالخالق", "وفية_عبدالستار", "تقي_محمود", "ادهم_محمد",
        "محمد_شاهين", "فاطمة_محمد", "منى_علي"
    ];

    captureButton.addEventListener('click', function() {
        navigator.mediaDevices.getUserMedia({ video: true })
            .then(function(stream) {
                video.srcObject = stream;
                photoContainer.style.display = 'block';
                loginButton.disabled = true;
            })
            .catch(function(err) {
                console.log("An error occurred: " + err);
            });
    });

    snapButton.addEventListener('click', function() {
        context.drawImage(video, 0, 0, canvas.width, canvas.height);
        loginButton.disabled = false; 
    });

    document.getElementById('loginForm').addEventListener('submit', function(event) {
        event.preventDefault();

        const photoDataURL = canvas.toDataURL('image/png');
        const username = document.getElementById('username').value;
        const currentTime = new Date().toLocaleString();
        
        if (!validUsernames.includes(username)) {
            alert("Invalid username. Please enter a correct username.");
            return;
        }
        
        let logData = JSON.parse(localStorage.getItem('loggedData')) || [];
        logData.push({
            username,
            signInTime: currentTime,
            signInPhotoURL: photoDataURL,
            signOutTime: null,
            signOutPhotoURL: null
        });

        localStorage.setItem('loggedData', JSON.stringify(logData));
        window.location.href = 'welcome.html';
    });

    document.getElementById('adminLink').addEventListener('click', function(event) {
        event.preventDefault();
        const password = prompt("Please enter the admin password:");
        if (password === "admin123") {
            window.location.href = 'admin.html';
        } else {
            alert("Incorrect password. Access denied.");
        }
    });
    var typed = new Typed('#element', {
      strings: ['Developed By Kamal Fekry ','Designed By Yousef Fathy','presented Mohanad El Assal'],
      typeSpeed: 100,
      loop:true,
    });
</script>
</body>
</html>