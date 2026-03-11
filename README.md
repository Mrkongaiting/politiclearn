# 袁心悦老师爱岗敬业，甘为铺路石、勇当大先生
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>十四五规划成果展示平台</title>
    <!-- 引入外部资源 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
    <!-- 新增3D效果库 -->
    <script src="https://cdn.jsdelivr.net/npm/three@0.154.0/build/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/countup.js@2.8.0/dist/countUp.umd.min.js"></script>
    
    <style>
        /* 全局3D效果增强 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            perspective: 1200px;
            scroll-behavior: smooth;
        }
        
        body {
            font-family: "Microsoft YaHei", "PingFang SC", sans-serif;
            background: linear-gradient(135deg, #001224 0%, #00284d 50%, #004080 100%);
            color: #fff;
            overflow-x: hidden;
            position: relative;
        }
        
        /* 粒子背景容器 */
        #particle-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
        }
        
        /* 3D背景装饰增强 */
        .bg-3d {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(circle at 20% 30%, rgba(255, 193, 7, 0.15) 0%, transparent 25%),
                radial-gradient(circle at 80% 70%, rgba(255, 193, 7, 0.15) 0%, transparent 25%),
                linear-gradient(135deg, #001224 0%, #00284d 50%, #004080 100%);
            transform-style: preserve-3d;
            animation: bgRotate 25s infinite linear alternate;
            backdrop-filter: blur(2px);
        }
        
        @keyframes bgRotate {
            0% { transform: rotateX(0deg) rotateY(0deg) translateZ(-50px); }
            100% { transform: rotateX(8deg) rotateY(8deg) translateZ(-50px); }
        }
        
        /* 导航栏3D效果 */
        .navbar-3d {
            background: rgba(0, 20, 40, 0.85);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(255, 193, 7, 0.2);
            transform-style: preserve-3d;
            transform: translateZ(50px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            z-index: 1000;
        }
        
        .nav-link {
            color: #e0e0e0 !important;
            transition: all 0.3s ease;
            transform-style: preserve-3d;
            position: relative;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 3px;
            background: linear-gradient(90deg, #ffc107, #ff8c00);
            border-radius: 3px;
            transition: width 0.3s ease;
            transform: translateZ(1px);
        }
        
        .nav-link:hover {
            color: #ffc107 !important;
            transform: translateZ(10px) translateY(-2px);
        }
        
        .nav-link:hover::after {
            width: 100%;
        }
        
        /* 轮播图3D效果增强 */
        .carousel-container {
            transform-style: preserve-3d;
            transform: perspective(2000px) rotateY(0deg);
            transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            margin-top: 70px;
        }
        
        .carousel-container:hover {
            transform: perspective(2000px) rotateY(5deg) rotateX(2deg);
        }
        
        .carousel-item {
            height: 90vh;
            min-height: 650px;
            transform-style: preserve-3d;
            position: relative;
        }
        
        .carousel-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, rgba(0,0,0,0.2), rgba(0,10,30,0.8));
            z-index: 1;
            transform: translateZ(-1px);
        }
        
        .carousel-item img {
            object-fit: cover;
            height: 100%;
            filter: brightness(0.8) contrast(1.1) saturate(1.2);
            transform: translateZ(-80px) scale(1.15);
            transition: all 1s ease;
        }
        
        .carousel-item:hover img {
            transform: translateZ(-60px) scale(1.12);
        }
        
        .carousel-caption {
            bottom: 30%;
            z-index: 10;
            text-shadow: 0 8px 20px rgba(0,0,0,0.9);
            transform: translateZ(50px);
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateZ(50px) translateY(0); }
            50% { transform: translateZ(50px) translateY(-15px); }
        }
        
        .carousel-caption h1 {
            font-size: 4.5rem;
            margin-bottom: 25px;
            text-transform: uppercase;
            letter-spacing: 3px;
            animation: textGlow 4s infinite alternate;
            font-weight: 700;
        }
        
        @keyframes textGlow {
            0% { text-shadow: 0 0 15px #ffc107, 0 8px 25px rgba(0,0,0,0.9); }
            100% { text-shadow: 0 0 30px #ffc107, 0 8px 35px rgba(0,0,0,0.9), 0 0 50px rgba(255,193,7,0.5); }
        }
        
        .carousel-caption p {
            font-size: 1.8rem;
            max-width: 1000px;
            margin: 0 auto;
            line-height: 1.6;
        }
        
        /* 展馆通用3D样式增强 */
        .museum-section {
            padding: 120px 0;
            min-height: 100vh;
            transform-style: preserve-3d;
            position: relative;
        }
        
        .museum-section::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 80%;
            height: 80%;
            background: radial-gradient(circle, rgba(255,193,7,0.05) 0%, transparent 70%);
            border-radius: 50%;
            transform: translate(-50%, -50%) translateZ(-10px);
            z-index: -1;
        }
        
        .museum-title {
            font-size: 3.8rem;
            color: #ffc107;
            margin-bottom: 80px;
            text-align: center;
            font-weight: bold;
            position: relative;
            transform: translateZ(50px);
            text-shadow: 0 5px 15px rgba(0,0,0,0.6);
            animation: titleFloat 5s ease-in-out infinite;
        }
        
        @keyframes titleFloat {
            0%, 100% { transform: translateZ(50px) translateY(0); }
            50% { transform: translateZ(50px) translateY(-10px); }
        }
        
        .museum-title::after {
            content: "";
            display: block;
            width: 120px;
            height: 6px;
            background: linear-gradient(90deg, #ffc107, #ff8c00);
            margin: 30px auto 0;
            border-radius: 3px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.4);
            transform: translateZ(1px);
        }
        
        /* 3D卡片样式增强 */
        .content-card {
            background: rgba(255, 255, 255, 0.06);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
            padding: 50px;
            margin-bottom: 50px;
            transform-style: preserve-3d;
            transform: translateZ(15px) rotateX(0deg) rotateY(0deg);
            transition: all 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        
        .content-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.05), transparent);
            transition: left 1.5s ease;
            z-index: 1;
        }
        
        .content-card:hover::before {
            left: 100%;
        }
        
        .content-card:hover {
            transform: translateZ(50px) translateY(-20px) rotateX(8deg) rotateY(5deg);
            box-shadow: 0 40px 80px rgba(0, 0, 0, 0.4);
            border-color: rgba(255, 193, 7, 0.3);
        }
        
        .content-card h3 {
            transform: translateZ(10px);
            margin-bottom: 25px;
            position: relative;
            padding-bottom: 15px;
        }
        
        .content-card h3::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 60px;
            height: 4px;
            background: linear-gradient(90deg, #ffc107, #ff8c00);
            border-radius: 2px;
            transform: translateZ(1px);
        }
        
        /* 数字滚动3D效果 */
        .counter-box {
            background: rgba(0, 20, 40, 0.5);
            border-radius: 15px;
            padding: 25px;
            margin: 20px 0;
            transform-style: preserve-3d;
            transform: translateZ(10px);
            border: 1px solid rgba(255, 193, 7, 0.2);
            text-align: center;
        }
        
        .counter-number {
            font-size: 3rem;
            font-weight: bold;
            color: #ffc107;
            text-shadow: 0 0 15px rgba(255,193,7,0.4);
            margin-bottom: 10px;
            transform: translateZ(5px);
        }
        
        .counter-label {
            font-size: 1.1rem;
            color: #e0e0e0;
            transform: translateZ(3px);
        }
        
        /* 财富馆样式增强 */
        .wealth-gif {
            width: 100%;
            border-radius: 20px;
            margin-bottom: 35px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
            transform: translateZ(10px);
            transition: transform 0.8s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .content-card:hover .wealth-gif {
            transform: translateZ(25px) scale(1.05);
        }
        
        .economic-data {
            font-size: 1.25rem;
            line-height: 1.9;
            margin-bottom: 25px;
            color: #e0e0e0;
            transform: translateZ(5px);
        }
        
        .data-highlight {
            color: #ffc107;
            font-weight: bold;
            font-size: 1.5rem;
            text-shadow: 0 0 15px rgba(255, 193, 7, 0.6);
            position: relative;
        }
        
        .data-highlight::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 2px;
            background: #ffc107;
            border-radius: 1px;
            transform: translateZ(1px);
        }
        
        /* 改革馆3D图片容器增强 */
        .reform-img-container {
            overflow: hidden;
            border-radius: 20px;
            height: 350px;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
            transform-style: preserve-3d;
            transform: translateZ(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .reform-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 1s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            transform: translateZ(0px) scale(1);
        }
        
        .reform-img-container:hover .reform-img {
            transform: translateZ(20px) scale(1.15) rotate(3deg);
            filter: brightness(1.1) contrast(1.1);
        }
        
        /* 民生馆样式增强 */
        .people-content {
            font-size: 1.25rem;
            line-height: 2.1;
            text-align: justify;
            color: #e0e0e0;
            transform: translateZ(5px);
        }
        
        .people-quote {
            font-style: italic;
            color: #ffc107;
            font-size: 1.6rem;
            margin: 50px 0;
            padding: 40px;
            border-left: 8px solid #ffc107;
            background: rgba(255, 193, 7, 0.15);
            backdrop-filter: blur(8px);
            border-radius: 0 20px 20px 0;
            transform: translateZ(15px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.25);
            position: relative;
        }
        
        .people-quote::before {
            content: '\201C';
            font-size: 5rem;
            color: rgba(255, 193, 7, 0.2);
            position: absolute;
            top: 10px;
            left: 20px;
            font-family: serif;
        }
        
        /* 交互按钮样式增强 */
        .btn-custom {
            background: linear-gradient(135deg, #ffc107, #ff8c00);
            border: none;
            border-radius: 50px;
            padding: 15px 40px;
            font-size: 1.25rem;
            font-weight: bold;
            color: #001f3f;
            box-shadow: 0 12px 25px rgba(255, 193, 7, 0.4);
            transform-style: preserve-3d;
            transform: translateZ(10px);
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        
        .btn-custom::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.8s ease;
            z-index: 1;
        }
        
        .btn-custom:hover::before {
            left: 100%;
        }
        
        .btn-custom:hover {
            transform: translateZ(20px) translateY(-5px) scale(1.05);
            box-shadow: 0 20px 40px rgba(255, 193, 7, 0.5);
            color: #001f3f;
        }
        
        .btn-custom:active {
            transform: translateZ(15px) translateY(-2px) scale(0.98);
            box-shadow: 0 10px 20px rgba(255, 193, 7, 0.4);
        }
        
        /* 数据图表样式增强 */
        .chart-container {
            width: 100%;
            height: 350px;
            margin: 40px 0;
            transform: translateZ(10px);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
            background: rgba(0, 20, 40, 0.4);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            padding: 20px;
        }
        
        /* 新增数据看板样式 */
        .data-dashboard {
            background: rgba(0, 20, 40, 0.4);
            backdrop-filter: blur(10px);
            border-radius: 25px;
            padding: 40px;
            margin-bottom: 50px;
            transform-style: preserve-3d;
            transform: translateZ(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
        }
        
        .dashboard-title {
            font-size: 2rem;
            color: #ffc107;
            margin-bottom: 30px;
            text-align: center;
            transform: translateZ(5px);
        }
        
        /* 回到顶部按钮3D样式增强 */
        .back-to-top {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: linear-gradient(135deg, #0056b3, #003366);
            color: #ffc107;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
            border: 2px solid #ffc107;
            transform-style: preserve-3d;
            transform: translateZ(10px);
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 999;
            cursor: pointer;
        }
        
        .back-to-top:hover {
            transform: translateZ(20px) rotateY(180deg) scale(1.1);
            background: linear-gradient(135deg, #ffc107, #ff8c00);
            color: #003366;
            box-shadow: 0 20px 40px rgba(255, 193, 7, 0.4);
        }
        
        /* 模态框样式增强 */
        .modal-content {
            background: rgba(0, 20, 40, 0.95) !important;
            backdrop-filter: blur(20px) !important;
            border-radius: 25px !important;
            border: 1px solid rgba(255, 193, 7, 0.3) !important;
            transform-style: preserve-3d !important;
            transform: translateZ(100px) !important;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.5) !important;
        }
        
        .modal-header {
            border-bottom: 1px solid rgba(255, 193, 7, 0.2) !important;
            padding: 30px !important;
        }
        
        .modal-body {
            padding: 30px !important;
            transform: translateZ(5px) !important;
        }
        
        .modal-footer {
            border-top: 1px solid rgba(255, 193, 7, 0.2) !important;
            padding: 20px 30px !important;
        }
        
        .modal img {
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            transform: translateZ(5px);
            margin-bottom: 25px;
        }
        
        /* 页脚样式增强 */
        footer {
            background: rgba(0, 10, 30, 0.9);
            backdrop-filter: blur(15px);
            color: white;
            padding: 80px 0 40px;
            margin-top: 100px;
            border-top: 1px solid rgba(255, 193, 7, 0.2);
            transform-style: preserve-3d;
            transform: translateZ(10px);
        }
        
        .footer-links a {
            color: #e0e0e0;
            margin: 0 15px;
            transition: all 0.3s ease;
            transform: translateZ(2px);
        }
        
        .footer-links a:hover {
            color: #ffc107;
            transform: translateZ(5px) translateY(-2px);
            text-decoration: none;
        }
        
        /* 响应式适配增强 */
        @media (max-width: 1200px) {
            .carousel-caption h1 {
                font-size: 3.8rem;
            }
            
            .museum-title {
                font-size: 3.2rem;
            }
        }
        
        @media (max-width: 992px) {
            .carousel-item {
                height: 75vh;
                min-height: 550px;
            }
            
            .carousel-caption h1 {
                font-size: 3rem;
            }
            
            .carousel-caption p {
                font-size: 1.5rem;
            }
            
            .museum-title {
                font-size: 2.8rem;
            }
            
            .content-card {
                padding: 40px;
            }
            
            .counter-number {
                font-size: 2.5rem;
            }
        }
        
        @media (max-width: 768px) {
            .carousel-item {
                height: 65vh;
                min-height: 450px;
            }
            
            .carousel-caption {
                bottom: 20%;
            }
            
            .carousel-caption h1 {
                font-size: 2.2rem;
            }
            
            .museum-section {
                padding: 80px 0;
            }
            
            .content-card {
                padding: 30px;
            }
            
            .reform-img-container {
                height: 280px;
            }
            
            .chart-container {
                height: 300px;
            }
            
            .counter-number {
                font-size: 2rem;
            }
        }
        
        @media (max-width: 576px) {
            .carousel-item {
                height: 55vh;
                min-height: 400px;
            }
            
            .carousel-caption h1 {
                font-size: 1.8rem;
            }
            
            .carousel-caption p {
                font-size: 1.2rem;
            }
            
            .museum-title {
                font-size: 2.2rem;
                margin-bottom: 50px;
            }
            
            .content-card {
                padding: 25px;
            }
            
            .btn-custom {
                padding: 12px 30px;
                font-size: 1.1rem;
            }
            
            .back-to-top {
                width: 60px;
                height: 60px;
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <!-- 粒子背景 -->
    <div id="particle-bg"></div>
    
    <!-- 3D背景 -->
    <div class="bg-3d"></div>

    <!-- 导航栏 -->
    <nav class="navbar navbar-expand-lg navbar-dark navbar-3d fixed-top">
        <div class="container">
            <a class="navbar-brand fw-bold fs-4" href="#home" style="color: #ffc107; transform: translateZ(10px);">
                <i class="bi bi-flag-fill me-2"></i>十四五规划成果展示
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
                <ul class="navbar-nav gap-4">
                    <li class="nav-item">
                        <a class="nav-link" href="#home">首页</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#wealth">财富馆</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#reform">改革馆</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#people">民生馆</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#data-center">数据中心</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- 首页轮播 -->
    <section id="home" class="carousel slide carousel-container" data-bs-ride="carousel" data-bs-interval="6000">
        <div class="carousel-indicators">
            <button type="button" data-bs-target="#home" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
            <button type="button" data-bs-target="#home" data-bs-slide-to="1" aria-label="Slide 2"></button>
            <button type="button" data-bs-target="#home" data-bs-slide-to="2" aria-label="Slide 3"></button>
        </div>
        <div class="carousel-inner">
            <!-- 科技工作者画面 -->
            <div class="carousel-item active">
                <img src="https://images.pexels.com/photos/3760069/pexels-photo-3760069.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="d-block w-100" alt="科技工作者">
                <div class="carousel-caption d-none d-md-block">
                    <h1>科技引领 创新发展</h1>
                    <p>广大科技工作者攻坚克难，为十四五规划提供坚实科技支撑</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看财富成果</a>
                </div>
            </div>
            <!-- 教育工作者画面 -->
            <div class="carousel-item">
                <img src="https://images.pexels.com/photos/3747503/pexels-photo-3747503.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="d-block w-100" alt="教育工作者">
                <div class="carousel-caption d-none d-md-block">
                    <h1>教育为本 人才强国</h1>
                    <p>教育工作者辛勤耕耘，为国家发展培育栋梁之才</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看财富成果</a>
                </div>
            </div>
            <!-- 综合发展画面 -->
            <div class="carousel-item">
                <img src="https://images.pexels.com/photos/544269/pexels-photo-544269.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="d-block w-100" alt="十四五发展成果">
                <div class="carousel-caption d-none d-md-block">
                    <h1>十四五规划 成果斐然</h1>
                    <p>经济发展、改革开放、民生改善取得历史性成就</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看财富成果</a>
                </div>
            </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#home" data-bs-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#home" data-bs-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Next</span>
        </button>
    </section>

    <!-- 财富馆 -->
    <section id="wealth" class="museum-section">
        <div class="container">
            <h2 class="museum-title">财富馆 - 经济发展成果</h2>
            
            <!-- 数字看板 -->
            <div class="row mb-5">
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter1">0</div>
                        <div class="counter-label">长三角GDP(万亿元)</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter2">0</div>
                        <div class="counter-label">人均可支配收入(元)</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter3">0</div>
                        <div class="counter-label">城镇新增就业(万人)</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter4">0</div>
                        <div class="counter-label">脱贫人口(万人)</div>
                    </div>
                </div>
            </div>
            
            <div class="row">
                <div class="col-lg-6">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-warning">长三角经济发展成果</h3>
                        <!-- 匹配内容的经济数据图片（开源） -->
                        <img src="https://images.pexels.com/photos/164688/pexels-photo-164688.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="wealth-gif" alt="长三角经济数据展示">
                        <p class="economic-data">长三角地区经济体量已突破<span class="data-highlight">29万亿元</span>，超过发达国家韩国（约24万亿元），成为中国经济发展的重要引擎。</p>
                        <p class="economic-data">2024年长三角地区GDP增速达到<span class="data-highlight">5.8%</span>，高于全国平均水平，展现出强劲的发展韧性。</p>
                        <!-- 交互数据图表 -->
                        <div class="chart-container">
                            <canvas id="yangtzeChart"></canvas>
                        </div>
                    </div>
                </div>
                <div class="col-lg-6">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-warning">全国民生经济数据</h3>
                        <img src="https://images.pexels.com/photos/548307/pexels-photo-548307.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="wealth-gif" alt="民生经济数据展示">
                        <p class="economic-data">全国居民人均可支配收入达到<span class="data-highlight">49283元</span>，较2020年增长<span class="data-highlight">42.3%</span>。</p>
                        <p class="economic-data">城镇新增就业连续五年超过<span class="data-highlight">1100万人</span>，就业形势保持稳定。</p>
                        <p class="economic-data">全国居民消费价格指数（CPI）保持在<span class="data-highlight">2%左右</span>的温和区间，物价水平总体稳定。</p>
                        <p class="economic-data">脱贫攻坚成果持续巩固，全国农村贫困人口全部脱贫，贫困地区居民收入增速持续高于全国平均水平。</p>
                        <!-- 交互数据图表 -->
                        <div class="chart-container">
                            <canvas id="peopleEconomyChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 改革馆 -->
    <section id="reform" class="museum-section">
        <div class="container">
            <h2 class="museum-title">改革馆 - 改革开放新成就</h2>
            <div class="row">
                <!-- 海南岛封关运作 -->
                <div class="col-lg-4 col-md-6">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">海南岛封关运作</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/1450358/pexels-photo-1450358.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="海南岛封关运作">
                        </div>
                        <p>海南自由贸易港封关运作准备工作全面完成，实现"一线放开、二线管住"的监管模式，成为中国对外开放的新高地。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('hainan')">查看详情</button>
                    </div>
                </div>
                <!-- 无人机送外卖 -->
                <div class="col-lg-4 col-md-6">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">无人机送外卖</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/130879/pexels-photo-130879.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="无人机送外卖">
                        </div>
                        <p>无人机配送服务在全国多个城市落地应用，覆盖外卖、快递等多个领域，配送效率提升30%以上，降低人力成本约40%。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('drone')">查看详情</button>
                    </div>
                </div>
                <!-- 无人驾驶与机器人 -->
                <div class="col-lg-4 col-md-12">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">智能科技应用</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/1818604/pexels-photo-1818604.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="无人驾驶与春晚机器人">
                        </div>
                        <p>"萝卜快跑"无人驾驶服务已在全国10余个城市商业化运营，累计安全行驶里程突破800万公里。</p>
                        <p>春晚智能机器人展现中国人工智能技术的领先水平，涵盖服务、工业、特种等多个领域的机器人技术实现突破。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('ai')">查看详情</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 民生馆 -->
    <section id="people" class="museum-section">
        <div class="container">
            <h2 class="museum-title">民生馆 - 群众观点与群众路线</h2>
            <div class="row">
                <div class="col-lg-8 mx-auto">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-center text-warning">坚持以人民为中心的发展思想</h3>
                        <p class="people-content">
                            十四五规划始终坚持群众观点和群众路线，把实现好、维护好、发展好最广大人民根本利益作为发展的出发点和落脚点。通过一系列民生保障政策，不断满足人民日益增长的美好生活需要，让发展成果更多更公平惠及全体人民。
                        </p>
                        <p class="people-content">
                            在教育方面，全面落实"双减"政策，推进义务教育优质均衡发展，全国普惠性幼儿园覆盖率达到90.8%，九年义务教育巩固率保持在95%以上。在医疗方面，基本医疗保险参保率稳定在95%以上，国家医保药品目录动态调整，新增407种药品纳入医保报销范围。
                        </p>
                        <p class="people-quote">
                            "江山就是人民，人民就是江山。我们党始终与人民心连心、同呼吸、共命运，始终把人民对美好生活的向往作为奋斗目标。"
                        </p>
                        <p class="people-content">
                            在社会保障方面，基本养老保险参保人数达到10.5亿人，实现养老保险全国统筹，退休人员基本养老金连续19年上调。保障性住房建设加快推进，累计建设各类保障性住房和棚改安置住房超过5000万套，帮助近2亿群众实现"安居梦"。
                        </p>
                        <p class="people-content">
                            坚持群众路线，深入开展"我为群众办实事"实践活动，建立健全党员干部联系服务群众机制，解决群众急难愁盼问题超过1200万件，群众满意度持续提升，获得感、幸福感、安全感更加充实、更有保障、更可持续。
                        </p>
                        <button class="btn btn-custom mt-4 d-block mx-auto" onclick="showPeopleData()">查看民生数据详情</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 新增：数据中心 -->
    <section id="data-center" class="museum-section">
        <div class="container">
            <h2 class="museum-title">数据中心 - 可视化成果看板</h2>
            
            <div class="data-dashboard">
                <h3 class="dashboard-title">十四五核心指标完成情况</h3>
                <div class="row">
                    <div class="col-lg-6 mb-4">
                        <div class="chart-container">
                            <canvas id="completionChart"></canvas>
                        </div>
                    </div>
                    <div class="col-lg-6 mb-4">
                        <div class="chart-container">
                            <canvas id="sectorChart"></canvas>
                        </div>
                    </div>
                </div>
                
                <div class="row mt-4">
                    <div class="col-lg-12">
                        <div class="chart-container">
                            <canvas id="growthChart"></canvas>
                        </div>
                    </div>
                </div>
                
                <div class="text-center mt-4">
                    <button class="btn btn-custom" onclick="exportData()">导出数据报告</button>
                </div>
            </div>
        </div>
    </section>

    <!-- 详情模态框 -->
    <div class="modal fade" id="detailModal" tabindex="-1" aria-labelledby="detailModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-lg modal-xl">
            <div class="modal-content bg-dark bg-opacity-90 text-white border border-warning">
                <div class="modal-header border-bottom border-warning">
                    <h5 class="modal-title text-warning" id="detailModalLabel">详情信息</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" id="modalContent">
                    <!-- 动态内容将在这里显示 -->
                </div>
                <div class="modal-footer border-top border-warning">
                    <button type="button" class="btn btn-custom" data-bs-dismiss="modal">关闭</button>
                </div>
            </div>
        </div>
    </div>

    <!-- 页脚 -->
    <footer>
        <div class="container">
            <div class="row mb-5">
                <div class="col-lg-12 text-center footer-links">
                    <a href="#home"><i class="bi bi-house-door-fill me-1"></i>首页</a>
                    <a href="#wealth"><i class="bi bi-graph-up me-1"></i>财富馆</a>
                    <a href="#reform"><i class="bi bi-lightbulb-fill me-1"></i>改革馆</a>
                    <a href="#people"><i class="bi bi-people-fill me-1"></i>民生馆</a>
                    <a href="#data-center"><i class="bi bi-database-fill me-1"></i>数据中心</a>
                </div>
            </div>
            <div class="row">
                <div class="col-lg-12 text-center">
                    <p class="mb-4">© 2025 十四五规划成果展示平台 版权所有</p>
                    <p>坚持以人民为中心 · 推动高质量发展 · 全面建设社会主义现代化国家</p>
                </div>
            </div>
        </div>
    </footer>

    <!-- 回到顶部按钮 -->
    <div onclick="window.scrollTo({top: 0, behavior: 'smooth'})" class="back-to-top">
        <i class="bi bi-arrow-up"></i>
    </div>

    <script>
        // 初始化粒子背景
        function initParticles() {
            const container = document.getElementById('particle-bg');
            if (!container) return;
            
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            container.appendChild(renderer.domElement);
            
            // 创建粒子
            const particlesGeometry = new THREE.BufferGeometry();
            const particlesCount = 1500;
            const posArray = new Float32Array(particlesCount * 3);
            
            for (let i = 0; i < particlesCount * 3; i++) {
                posArray[i] = (Math.random() - 0.5) * 10;
            }
            
            particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
            
            // 粒子材质
            const particlesMaterial = new THREE.PointsMaterial({
                size: 0.02,
                color: 0xffc107,
                transparent: true,
                opacity: 0.6
            });
            
            const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
            scene.add(particlesMesh);
            
            camera.position.z = 3;
            
            // 动画循环
            function animate() {
                requestAnimationFrame(animate);
                particlesMesh.rotation.x += 0.0005;
                particlesMesh.rotation.y += 0.0005;
                renderer.render(scene, camera);
            }
            
            animate();
            
            // 窗口大小调整
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
        }
        
        // 鼠标交互3D背景
        document.addEventListener('mousemove', function(e) {
            const bg = document.querySelector('.bg-3d');
            if (bg) {
                const x = e.clientX / window.innerWidth - 0.5;
                const y = e.clientY / window.innerHeight - 0.5;
                bg.style.transform = `rotateX(${y * 8}deg) rotateY(${x * 8}deg) translateZ(-50px)`;
            }
        });

        // 数字滚动效果
        function initCounters() {
            const options = {
                duration: 3,
                useEasing: true,
                useGrouping: true,
                separator: ',',
                decimal: '.',
            };
            
            const counter1 = new countUp.CountUp('counter1', 29, options);
            const counter2 = new countUp.CountUp('counter2', 49283, options);
            const counter3 = new countUp.CountUp('counter3', 1100, options);
            const counter4 = new countUp.CountUp('counter4', 9899, options);
            
            // 滚动到财富馆时触发数字滚动
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        counter1.start();
                        counter2.start();
                        counter3.start();
                        counter4.start();
                        observer.disconnect();
                    }
                });
            }, { threshold: 0.2 });
            
            observer.observe(document.getElementById('wealth'));
        }

        // 长三角经济数据图表
        const yangtzeCtx = document.getElementById('yangtzeChart')?.getContext('2d');
        if (yangtzeCtx) {
            new Chart(yangtzeCtx, {
                type: 'bar',
                data: {
                    labels: ['2020', '2021', '2022', '2023', '2024'],
                    datasets: [{
                        label: '长三角GDP总量(万亿元)',
                        data: [23.7, 25.6, 27.1, 28.3, 29.0],
                        backgroundColor: 'rgba(255, 193, 7, 0.7)',
                        borderColor: 'rgba(255, 193, 7, 1)',
                        borderWidth: 1,
                        borderRadius: 8
                    }, {
                        label: '韩国GDP总量(万亿元)',
                        data: [20.5, 21.8, 22.5, 23.2, 24.0],
                        backgroundColor: 'rgba(108, 117, 125, 0.7)',
                        borderColor: 'rgba(108, 117, 125, 1)',
                        borderWidth: 1,
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            labels: {
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        title: {
                            display: true,
                            text: '长三角VS韩国GDP对比',
                            color: '#ffc107',
                            font: { size: 18, weight: 'bold' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 20, 40, 0.9)',
                            titleColor: '#ffc107',
                            bodyColor: '#fff',
                            borderColor: 'rgba(255, 193, 7, 0.3)',
                            borderWidth: 1,
                            padding: 15,
                            cornerRadius: 10
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#e0e0e0',
                                font: { size: 12 }
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#e0e0e0',
                                font: { size: 12 }
                            }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                }
            });
        }

        // 民生经济数据图表
        const peopleCtx = document.getElementById('peopleEconomyChart')?.getContext('2d');
        if (peopleCtx) {
            new Chart(peopleCtx, {
                type: 'line',
                data: {
                    labels: ['2020', '2021', '2022', '2023', '2024'],
                    datasets: [{
                        label: '居民人均可支配收入(元)',
                        data: [32189, 35128, 36883, 42833, 49283],
                        fill: true,
                        backgroundColor: 'rgba(255, 193, 7, 0.2)',
                        borderColor: 'rgba(255, 193, 7, 1)',
                        tension: 0.4,
                        pointBackgroundColor: '#ffc107',
                        pointRadius: 6,
                        pointHoverRadius: 8
                    }, {
                        label: 'CPI指数(%)',
                        data: [2.5, 0.9, 2.0, 2.1, 2.0],
                        fill: false,
                        borderColor: 'rgba(0, 191, 255, 1)',
                        tension: 0.4,
                        pointBackgroundColor: '#00bfff',
                        pointRadius: 6,
                        pointHoverRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            labels: {
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        title: {
                            display: true,
                            text: '民生经济数据趋势',
                            color: '#ffc107',
                            font: { size: 18, weight: 'bold' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 20, 40, 0.9)',
                            titleColor: '#ffc107',
                            bodyColor: '#fff',
                            borderColor: 'rgba(255, 193, 7, 0.3)',
                            borderWidth: 1,
                            padding: 15,
                            cornerRadius: 10
                        }
                    },
                    scales: {
                        y: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#e0e0e0',
                                font: { size: 12 }
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            ticks: {
                                color: '#e0e0e0',
                                font: { size: 12 }
                            }
                        }
                    },
                    animation: {
                        duration: 2000,
                        easing: 'easeOutQuart'
                    }
                }
            });
        }

        // 新增：完成率图表
        const completionCtx = document.getElementById('completionChart')?.getContext('2d');
        if (completionCtx) {
            new Chart(completionCtx, {
                type: 'radar',
                data: {
                    labels: ['经济增长', '就业保障', '科技创新', '民生改善', '绿色发展', '改革开放'],
                    datasets: [{
                        label: '目标值',
                        data: [100, 100, 100, 100, 100, 100],
                        backgroundColor: 'rgba(108, 117, 125, 0.2)',
                        borderColor: 'rgba(108, 117, 125, 0.8)',
                        pointBackgroundColor: '#6c757d',
                        pointRadius: 5
                    }, {
                        label: '完成值',
                        data: [105, 112, 120, 108, 115, 110],
                        backgroundColor: 'rgba(255, 193, 7, 0.2)',
                        borderColor: 'rgba(255, 193, 7, 0.8)',
                        pointBackgroundColor: '#ffc107',
                        pointRadius: 5
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        title: {
                            display: true,
                            text: '核心指标完成率',
                            color: '#ffc107',
                            font: { size: 16, weight: 'bold' }
                        }
                    },
                    scales: {
                        r: {
                            angleLines: { color: 'rgba(255,255,255,0.1)' },
                            grid: { color: 'rgba(255,255,255,0.1)' },
                            pointLabels: { color: '#e0e0e0', font: { size: 12 } },
                            ticks: {
                                color: '#e0e0e0',
                                backdropColor: 'transparent',
                                stepSize: 20
                            }
                        }
                    }
                }
            });
        }

        // 新增：产业结构图表
        const sectorCtx = document.getElementById('sectorChart')?.getContext('2d');
        if (sectorCtx) {
            new Chart(sectorCtx, {
                type: 'doughnut',
                data: {
                    labels: ['第一产业', '第二产业', '第三产业', '数字经济'],
                    datasets: [{
                        data: [7.3, 39.4, 48.8, 4.5],
                        backgroundColor: [
                            'rgba(40, 167, 69, 0.7)',
                            'rgba(0, 123, 255, 0.7)',
                            'rgba(255, 193, 7, 0.7)',
                            'rgba(220, 53, 69, 0.7)'
                        ],
                        borderColor: 'rgba(0, 20, 40, 0.8)',
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'right',
                            labels: { color: '#fff', font: { size: 14 } }
                        },
                        title: {
                            display: true,
                            text: '产业结构占比',
                            color: '#ffc107',
                            font: { size: 16, weight: 'bold' }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.label + ': ' + context.raw + '%';
                                }
                            }
                        }
                    },
                    cutout: '60%',
                    animation: {
                        animateRotate: true,
                        animateScale: true
                    }
                }
            });
        }

        // 新增：增长趋势图表
        const growthCtx = document.getElementById('growthChart')?.getContext('2d');
        if (growthCtx) {
            new Chart(growthCtx, {
                type: 'line',
                data: {
                    labels: ['2020', '2021', '2022', '2023', '2024'],
                    datasets: [{
                        label: 'GDP增长率(%)',
                        data: [2.3, 8.1, 3.0, 5.2, 5.8],
                        borderColor: '#ffc107',
                        backgroundColor: 'rgba(255, 193, 7, 0.1)',
                        fill: true,
                        tension: 0.3
                    }, {
                        label: '人均可支配收入增长率(%)',
                        data: [4.7, 9.1, 5.0, 6.3, 7.1],
                        borderColor: '#00bfff',
                        backgroundColor: 'rgba(0, 191, 255, 0.1)',
                        fill: true,
                        tension: 0.3
                    }, {
                        label: '固定资产投资增长率(%)',
                        data: [2.9, 4.9, 5.1, 4.5, 4.8],
                        borderColor: '#28a745',
                        backgroundColor: 'rgba(40, 167, 69, 0.1)',
                        fill: true,
                        tension: 0.3
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        title: {
                            display: true,
                            text: '关键指标增长趋势',
                            color: '#ffc107',
                            font: { size: 16, weight: 'bold' }
                        }
                    },
                    scales: {
                        y: {
                            grid: { color: 'rgba(255,255,255,0.1)' },
                            ticks: { color: '#e0e0e0' }
                        },
                        x: {
                            grid: { color: 'rgba(255,255,255,0.1)' },
                            ticks: { color: '#e0e0e0' }
                        }
                    }
                }
            });
        }

        // 详情展示函数
        function showDetail(type) {
            const modalTitle = document.getElementById('detailModalLabel');
            const modalContent = document.getElementById('modalContent');
            const modal = new bootstrap.Modal(document.getElementById('detailModal'));

            switch(type) {
                case 'hainan':
                    modalTitle.textContent = '海南岛封关运作详情';
                    modalContent.innerHTML = `
                        <img src="https://images.pexels.com/photos/1450358/pexels-photo-1450358.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="img-fluid rounded mb-3" alt="海南封关">
                        <p class="lead">海南自由贸易港封关运作于2025年正式实施，这是中国对外开放的重大举措。</p>
                        <ul class="list-group list-group-flush bg-transparent">
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 全岛封关运作，实现"一线放开、二线管住"的监管模式</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 零关税政策覆盖99%以上商品，打造国际消费中心</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 累计注册市场主体超300万户，年均增长30%以上</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 2024年海南GDP突破8000亿元，增速达9.2%</li>
                        </ul>
                    `;
                    break;
                case 'drone':
                    modalTitle.textContent = '无人机配送发展详情';
                    modalContent.innerHTML = `
                        <img src="https://images.pexels.com/photos/130879/pexels-photo-130879.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="img-fluid rounded mb-3" alt="无人机配送">
                        <p class="lead">无人机配送已成为智慧城市建设的重要组成部分，改变传统物流模式。</p>
                        <ul class="list-group list-group-flush bg-transparent">
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 全国已建成无人机配送航线超1000条，覆盖50余个城市</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 配送效率提升30%以上，人力成本降低约40%</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 单架无人机日均配送量达200单，覆盖半径15公里</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 2024年无人机配送市场规模突破200亿元</li>
                        </ul>
                    `;
                    break;
                case 'ai':
                    modalTitle.textContent = '智能科技应用详情';
                    modalContent.innerHTML = `
                        <img src="https://images.pexels.com/photos/1818604/pexels-photo-1818604.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="img-fluid rounded mb-3" alt="智能科技">
                        <p class="lead">中国智能科技发展走在世界前列，无人驾驶和机器人技术成果显著。</p>
                        <ul class="list-group list-group-flush bg-transparent">
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ "萝卜快跑"无人驾驶服务覆盖15个城市，累计行驶800万公里</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 春晚机器人涵盖服务、工业、特种等10余个品类，技术全球领先</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 2024年中国人工智能核心产业规模突破5000亿元</li>
                            <li class="list-group-item bg-transparent border-warning border-opacity-25">✓ 智能机器人年产量突破100万台，国产化率达85%</li>
                        </ul>
                    `;
                    break;
            }
            
            modal.show();
        }

        // 民生数据详情展示
        function showPeopleData() {
            const modalTitle = document.getElementById('detailModalLabel');
            const modalContent = document.getElementById('modalContent');
            const modal = new bootstrap.Modal(document.getElementById('detailModal'));

            modalTitle.textContent = '民生发展详细数据';
            modalContent.innerHTML = `
                <div class="row">
                    <div class="col-md-6">
                        <h5 class="text-warning mb-3">教育事业</h5>
                        <ul class="list-group list-group-flush bg-transparent">
                            <li class="list-group-item bg-transparent">普惠性幼儿园覆盖率：90.8%</li>
