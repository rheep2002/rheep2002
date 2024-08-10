html
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>التقاط صورة</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        video {
            border: 1px solid #ccc;
            margin-bottom: 10px;
        }
        img {
            margin-top: 10px;
            max-width: 100%;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body>

<video id="video" width="320" height="240" autoplay></video>
<button id="snap">التقاط صورة</button>
<canvas id="canvas" width="320" height="240" style="display:none;"></canvas>
<img id="photo" src="" alt="الصورة الملتقطة"/>

<script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('canvas');
    const context = canvas.getContext('2d');
    const photo = document.getElementById('photo');

    // الوصول إلى الكاميرا
    navigator.mediaDevices.getUserMedia({ video: true })
        .then(stream => {
            video.srcObject = stream;
        })
        .catch(err => {
            console.error("حدث خطأ:", err);
            alert("لا يمكن الوصول إلى الكاميرا. يرجى التأكد من أن لديك إذن الوصول.");
        });

    // التقاط الصورة عند الضغط على الزر
    document.getElementById('snap').addEventListener('click', () => {
        context.drawImage(video, 0, 0, 320, 240);
        photo.src = canvas.toDataURL('image/png');
    });
</script>

</body>
</html>
