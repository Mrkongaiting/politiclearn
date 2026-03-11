<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>十四五规划成果展示平台 | 教师编备考专题</title>
    <!-- 引入外部资源 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
    <!-- 新增3D效果库 -->
    <script src="https://cdn.jsdelivr.net/npm/three@0.154.0/build/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/countup.js@2.8.0/dist/countUp.umd.min.js"></script>
    <!-- 新增滚动视差库 -->
    <script src="https://cdn.jsdelivr.net/npm/parallax-js@3.1.0/dist/parallax.min.js"></script>
    
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
        
        /* 3D背景装饰增强 - 新增动态渐变+光影 */
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
            animation: bgRotate 25s infinite linear alternate, bgColorShift 15s infinite ease-in-out alternate;
            backdrop-filter: blur(2px);
            box-shadow: inset 0 0 200px rgba(0, 80, 160, 0.5);
        }
        
        /* 新增背景颜色渐变动画 */
        @keyframes bgColorShift {
            0% { background-position: 0% 50%; }
            100% { background-position: 100% 50%; }
        }
        
        @keyframes bgRotate {
            0% { transform: rotateX(0deg) rotateY(0deg) translateZ(-50px); }
            100% { transform: rotateX(8deg) rotateY(8deg) translateZ(-50px); }
        }
        
        /* 导航栏3D效果增强 - 新增悬浮光晕 */
        .navbar-3d {
            background: rgba(0, 20, 40, 0.85);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(255, 193, 7, 0.2);
            transform-style: preserve-3d;
            transform: translateZ(50px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3), 0 0 20px rgba(255, 193, 7, 0.1);
            z-index: 1000;
            transition: all 0.5s ease;
        }
        
        .navbar-3d.scrolled {
            background: rgba(0, 20, 40, 0.95);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5), 0 0 30px rgba(255, 193, 7, 0.2);
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
            text-shadow: 0 0 10px rgba(255, 193, 7, 0.5);
        }
        
        .nav-link:hover::after {
            width: 100%;
        }
        
        /* 轮播图3D效果增强 - 新增视差+光影 */
        .carousel-container {
            transform-style: preserve-3d;
            transform: perspective(2000px) rotateY(0deg);
            transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            margin-top: 70px;
            position: relative;
        }
        
        .carousel-container::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100px;
            background: linear-gradient(to top, #001224, transparent);
            z-index: 5;
            transform: translateZ(1px);
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
        
        /* 展馆通用3D样式增强 - 新增滚动视差 */
        .museum-section {
            padding: 120px 0;
            min-height: 100vh;
            transform-style: preserve-3d;
            position: relative;
            scroll-snap-align: start;
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
            animation: linePulse 3s infinite alternate;
        }
        
        /* 新增标题下划线脉冲动画 */
        @keyframes linePulse {
            0% { width: 120px; opacity: 0.8; }
            100% { width: 180px; opacity: 1; }
        }
        
        /* 3D卡片样式增强 - 新增GIF动图容器+光影分层 */
        .content-card {
            background: rgba(255, 255, 255, 0.06);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25), 0 0 30px rgba(0, 80, 160, 0.1);
            padding: 50px;
            margin-bottom: 50px;
            transform-style: preserve-3d;
            transform: translateZ(15px) rotateX(0deg) rotateY(0deg);
            transition: all 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        
        /* 新增卡片高光效果 */
        .content-card::after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 40%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.03), transparent);
            transform: skewX(-20deg) translateX(100%);
            transition: transform 1.5s ease;
            z-index: 1;
        }
        
        .content-card:hover::after {
            transform: skewX(-20deg) translateX(-100%);
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
            box-shadow: 0 40px 80px rgba(0, 0, 0, 0.4), 0 0 50px rgba(255, 193, 7, 0.1);
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
        
        /* GIF动图容器增强 - 新增3D边框+悬浮缩放 */
        .gif-container {
            position: relative;
            border-radius: 20px;
            overflow: hidden;
            margin-bottom: 35px;
            transform-style: preserve-3d;
            transform: translateZ(10px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
            border: 2px solid transparent;
            background: linear-gradient(rgba(0,20,40,0.8), rgba(0,20,40,0.8)) padding-box,
                        linear-gradient(135deg, #ffc107, #ff8c00, #007bff) border-box;
            transition: all 0.8s ease;
        }
        
        .gif-container:hover {
            transform: translateZ(25px) scale(1.02);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5), 0 0 40px rgba(255, 193, 7, 0.2);
        }
        
        .gif-container img, .gif-container iframe {
            width: 100%;
            display: block;
            transform: translateZ(5px);
        }
        
        /* 数字滚动3D效果增强 */
        .counter-box {
            background: rgba(0, 20, 40, 0.5);
            border-radius: 15px;
            padding: 25px;
            margin: 20px 0;
            transform-style: preserve-3d;
            transform: translateZ(10px);
            border: 1px solid rgba(255, 193, 7, 0.2);
            text-align: center;
            transition: all 0.5s ease;
        }
        
        .counter-box:hover {
            transform: translateZ(20px) scale(1.05);
            border-color: rgba(255, 193, 7, 0.5);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
        }
        
        .counter-number {
            font-size: 3rem;
            font-weight: bold;
            color: #ffc107;
            text-shadow: 0 0 15px rgba(255,193,7,0.4);
            margin-bottom: 10px;
            transform: translateZ(5px);
            animation: numberGlow 2s infinite alternate;
        }
        
        @keyframes numberGlow {
            0% { text-shadow: 0 0 15px rgba(255,193,7,0.4); }
            100% { text-shadow: 0 0 25px rgba(255,193,7,0.8); }
        }
        
        .counter-label {
            font-size: 1.1rem;
            color: #e0e0e0;
            transform: translateZ(3px);
        }
        
        /* 经济数据样式增强 */
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
            animation: highlightPulse 2s infinite alternate;
        }
        
        @keyframes highlightPulse {
            0% { text-shadow: 0 0 15px rgba(255, 193, 7, 0.6); }
            100% { text-shadow: 0 0 25px rgba(255, 193, 7, 0.9); }
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
            transition: all 0.8s ease;
        }
        
        .reform-img-container:hover {
            transform: translateZ(20px) scale(1.03);
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
            transition: all 0.5s ease;
        }
        
        .people-quote:hover {
            transform: translateZ(25px) translateX(10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.35);
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
            transition: all 0.5s ease;
        }
        
        .chart-container:hover {
            transform: translateZ(20px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
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
            opacity: 0;
            visibility: hidden;
        }
        
        .back-to-top.visible {
            opacity: 1;
            visibility: visible;
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
            text-shadow: 0 0 10px rgba(255, 193, 7, 0.5);
        }
        
        /* 新增滚动条美化 */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(0, 20, 40, 0.5);
        }
        
        ::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #ffc107, #ff8c00);
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(135deg, #ff8c00, #ffc107);
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
                <i class="bi bi-flag-fill me-2"></i>教师编备考 | 一战上岸
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
                        <a class="nav-link" href="#wealth">备考成果</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#reform">备考攻略</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#people">备考心得</a>
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
                <img src="https://q3.itc.cn/images01/20240508/849d10228e144baaab73de03bd84e8e1.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="d-block w-100" alt="教师备考">
                <div class="carousel-caption d-none d-md-block">
                    <h1>拼搏奋发 一战上岸</h1>
                    <p>精心备考，为教师编考试筑牢坚实基础</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看备考成果</a>
                </div>
            </div>
            <!-- 教育工作者画面 -->
            <div class="carousel-item">
                <img src="https://images.pexels.com/photos/3747503/pexels-photo-3747503.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="d-block w-100" alt="教育工作者">
                <div class="carousel-caption d-none d-md-block">
                    <h1>教育为本 人才强国</h1>
                    <p>成为优秀教育工作者，为国家发展培育栋梁之才</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看备考成果</a>
                </div>
            </div>
            <!-- 综合发展画面 -->
            <div class="carousel-item">
                <img src="https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/9423&x-signature=Hv2tlTaxRoYbhfNwhNbyddjhw%2F4%3D" class="d-block w-100" alt="上岸大湾区">
                <div class="carousel-caption d-none d-md-block">
                    <h1>上岸大湾区 拼在当下</h1>
                    <p>苏锡常、杭嘉甬、大湾区教师编备考全攻略</p>
                    <a href="#wealth" class="btn btn-custom mt-4">查看备考成果</a>
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

    <!-- 备考成果馆 -->
    <section id="wealth" class="museum-section">
        <div class="container">
            <h2 class="museum-title">教师编 - 2026年一战上岸！</h2>
            
            <!-- 数字看板 -->
            <div class="row mb-5">
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter1">1</div>
                        <div class="counter-label">苏锡常教师编(长三角)</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter2">100%</div>
                        <div class="counter-label">杭嘉甬考点全覆盖</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter3">98</div>
                        <div class="counter-label">广州深圳大湾区模拟分</div>
                    </div>
                </div>
                <div class="col-lg-3 col-md-6 mb-4">
                    <div class="counter-box">
                        <div class="counter-number" id="counter4">4</div>
                        <div class="counter-label">教育综合知识过轮数</div>
                    </div>
                </div>
            </div>
            
            <div class="row">
                <div class="col-lg-6">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-warning">备考成果</h3>
                        <!-- 备考学习GIF动图 -->
                        <div class="gif-container">
                            <img src="https://cdn.pixabay.com/animation/2023/06/10/10/39/10-39-24-985_512.gif" alt="备考学习动图">
                        </div>
                        <p class="economic-data">教育综合知识已过掉<span class="data-highlight">4轮</span>，知识点掌握率达到95%以上，远超平均备考水平。</p>
                        <p class="economic-data">2024-2025备考周期内，模拟考试平均分达到<span class="data-highlight">92分</span>，较初始阶段提升40%。</p>
                        <!-- 交互数据图表 -->
                        <div class="chart-container">
                            <canvas id="yangtzeChart"></canvas>
                        </div>
                    </div>
                </div>
                <div class="col-lg-6">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-warning">备考进度数据</h3>
                        <!-- 时间规划GIF动图 -->
                        <div class="gif-container">
                            <img src="https://cdn.pixabay.com/animation/2023/07/10/12/59/12-59-27-888_512.gif" alt="时间规划动图">
                        </div>
                        <p class="economic-data">每日有效学习时长达到<span class="data-highlight">8小时</span>，周末加练2小时，累计学习时长超1200小时。</p>
                        <p class="economic-data">刷题量突破<span class="data-highlight">11000道</span>，错题率从初始45%降至当前8%。</p>
                        <p class="economic-data">主观题答题完整率保持在<span class="data-highlight">95%以上</span>，答题规范度持续提升。</p>
                        <p class="economic-data">面试模拟练习累计<span class="data-highlight">50次</span>，表达流畅度和逻辑性显著提高。</p>
                        <!-- 交互数据图表 -->
                        <div class="chart-container">
                            <canvas id="peopleEconomyChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 备考攻略馆 -->
    <section id="reform" class="museum-section">
        <div class="container">
            <h2 class="museum-title">备考攻略 - 高效备考新方法</h2>
            <div class="row">
                <!-- 考点分析 -->
                <div class="col-lg-4 col-md-6">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">考点精准分析</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/1450358/pexels-photo-1450358.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="考点分析">
                        </div>
                        <p>对苏锡常、杭嘉甬、大湾区三地近5年真题进行深度分析，提炼高频考点86个，精准覆盖考试范围98%以上。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('hainan')">查看详情</button>
                    </div>
                </div>
                <!-- 智能刷题 -->
                <div class="col-lg-4 col-md-6">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">智能刷题系统</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/130879/pexels-photo-130879.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="智能刷题">
                        </div>
                        <p>使用AI智能刷题系统，根据错题自动生成个性化练习计划，刷题效率提升30%以上，错题复现率降低40%。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('drone')">查看详情</button>
                    </div>
                </div>
                <!-- 模拟面试 -->
                <div class="col-lg-4 col-md-12">
                    <div class="content-card h-100">
                        <h3 class="h4 mb-4 text-warning">全真模拟面试</h3>
                        <div class="reform-img-container">
                            <img src="https://images.pexels.com/photos/1818604/pexels-photo-1818604.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" class="reform-img" alt="模拟面试">
                        </div>
                        <p>采用AI面试评分系统+真人考官双模式，累计模拟面试50场，涵盖结构化、试讲、答辩全流程，评分准确率达90%以上。</p>
                        <button class="btn btn-custom mt-3" onclick="showDetail('ai')">查看详情</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 备考心得馆 -->
    <section id="people" class="museum-section">
        <div class="container">
            <h2 class="museum-title">备考心得 - 坚持与努力同行</h2>
            <div class="row">
                <div class="col-lg-8 mx-auto">
                    <div class="content-card">
                        <h3 class="h4 mb-4 text-center text-warning">坚持以目标为导向的备考理念</h3>
                        <!-- 励志GIF动图 -->
                        <div class="gif-container">
                            <img src="https://cdn.pixabay.com/animation/2023/08/06/07/05/07-05-44-628_512.gif" alt="励志动图">
                        </div>
                        <p class="people-content">
                            备考教师编的过程，是一场与自己的较量。我始终坚持每天8小时的有效学习时间，严格执行学习计划，把实现上岸目标作为一切行动的出发点和落脚点。通过系统化的知识点梳理、高强度的刷题训练、常态化的模拟面试，不断提升自己的综合应试能力。
                        </p>
                        <p class="people-content">
                            在学习方法上，我注重"理解+记忆+应用"三位一体，不仅掌握知识点本身，更注重知识点之间的关联和实际教学场景中的应用。通过错题本、思维导图、口诀记忆等多种方式，让抽象的教育理论变得具体可感，记忆效率提升60%以上。
                        </p>
                        <p class="people-quote">
                            "每一次的坚持都不会白费，每一滴的汗水都将浇灌出成功的花朵。上岸不是终点，而是成为优秀教育工作者的新起点。"
                        </p>
                        <p class="people-content">
                            备考过程中，我也注重心态的调整和压力的释放。每天保证1小时的运动时间，定期与备考伙伴交流心得，保持积极向上的备考状态。相信只要坚持正确的方法，付出足够的努力，2026年一战上岸的目标一定能够实现。
                        </p>
                        <button class="btn btn-custom mt-4 d-block mx-auto" onclick="showPeopleData()">查看备考数据详情</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 数据中心 -->
    <section id="data-center" class="museum-section">
        <div class="container">
            <h2 class="museum-title">数据中心 - 备考成果可视化看板</h2>
            
            <div class="data-dashboard">
                <h3 class="dashboard-title">备考核心指标完成情况</h3>
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
                    <button class="btn btn-custom" onclick="exportData()">导出备考报告</button>
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
                    <a href="#wealth"><i class="bi bi-graph-up me-1"></i>备考成果</a>
                    <a href="#reform"><i class="bi bi-lightbulb-fill me-1"></i>备考攻略</a>
                    <a href="#people"><i class="bi bi-people-fill me-1"></i>备考心得</a>
                    <a href="#data-center"><i class="bi bi-database-fill me-1"></i>数据中心</a>
                </div>
            </div>
            <div class="row">
                <div class="col-lg-12 text-center">
                    <p class="mb-4">© 2025 教师编备考平台 版权所有</p>
                    <p>坚持以目标为导向 · 推动高效备考 · 全力实现一战上岸</p>
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
            
            // 粒子材质 - 新增颜色渐变
            const particlesMaterial = new THREE.PointsMaterial({
                size: 0.02,
                color: 0xffc107,
                transparent: true,
                opacity: 0.6,
                sizeAttenuation: true
            });
            
            const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
            scene.add(particlesMesh);
            
            camera.position.z = 3;
            
            // 动画循环 - 新增鼠标交互
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
        
        // 鼠标交互3D背景 - 增强灵敏度
        document.addEventListener('mousemove', function(e) {
            const bg = document.querySelector('.bg-3d');
            if (bg) {
                const x = e.clientX / window.innerWidth - 0.5;
                const y = e.clientY / window.innerHeight - 0.5;
                bg.style.transform = `rotateX(${y * 10}deg) rotateY(${x * 10}deg) translateZ(-50px)`;
            }
        });

        // 数字滚动效果 - 修复数值匹配
        function initCounters() {
            const options = {
                duration: 3,
                useEasing: true,
                useGrouping: true,
                separator: ',',
                decimal: '.',
            };
            
            const counter1 = new countUp.CountUp('counter1', 1, options);
            const counter2 = new countUp.CountUp('counter2', 100, { ...options, suffix: '%' });
            const counter3 = new countUp.CountUp('counter3', 98, options);
            const counter4 = new countUp.CountUp('counter4', 4, options);
            
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

        // 导航栏滚动效果
        window.addEventListener('scroll', function() {
            const navbar = document.querySelector('.navbar-3d');
            const backToTop = document.querySelector('.back-to-top');
            
            if (window.scrollY > 100) {
                navbar.classList.add('scrolled');
                backToTop.classList.add('visible');
            } else {
                navbar.classList.remove('scrolled');
                backToTop.classList.remove('visible');
            }
        });

        // 备考进度图表
        const yangtzeCtx = document.getElementById('yangtzeChart')?.getContext('2d');
        if (yangtzeCtx) {
            new Chart(yangtzeCtx, {
                type: 'bar',
                data: {
                    labels: ['第一轮', '第二轮', '第三轮', '第四轮'],
                    datasets: [{
                        label: '知识点掌握率(%)',
                        data: [65, 78, 88, 95],
                        backgroundColor: 'rgba(255, 193, 7, 0.7)',
                        borderColor: 'rgba(255, 193, 7, 1)',
                        borderWidth: 1,
                        borderRadius: 8
                    }, {
                        label: '答题正确率(%)',
                        data: [55, 70, 82, 90],
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
                            text: '备考四轮知识点掌握情况',
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
                            max: 100,
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

        // 学习时长图表
        const peopleCtx = document.getElementById('peopleEconomyChart')?.getContext('2d');
        if (peopleCtx) {
            new Chart(peopleCtx, {
                type: 'line',
                data: {
                    labels: ['1月', '2月', '3月', '4月', '5月'],
                    datasets: [{
                        label: '月均学习时长(小时)',
                        data: [180, 200, 220, 240, 260],
                        fill: true,
                        backgroundColor: 'rgba(255, 193, 7, 0.2)',
                        borderColor: 'rgba(255, 193, 7, 1)',
                        tension: 0.4,
                        pointBackgroundColor: '#ffc107',
                        pointRadius: 6,
                        pointHoverRadius: 8
                    }, {
                        label: '错题率(%)',
                        data: [45, 35, 20, 12, 8],
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
                            text: '备考时长与错题率趋势',
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

        // 完成率图表
        const completionCtx = document.getElementById('completionChart')?.getContext('2d');
        if (completionCtx) {
            new Chart(completionCtx, {
                type: 'radar',
                data: {
                    labels: ['知识点掌握', '刷题量', '模拟考试', '面试练习', '错题复盘', '计划执行'],
                    datasets: [{
                        label: '目标值',
                        data: [100, 100, 100, 100, 100, 100],
                        backgroundColor: 'rgba(108, 117, 125, 0.2)',
                        borderColor: 'rgba(108, 117, 125, 0.8)',
                        pointBackgroundColor: '#6c757d',
                        pointRadius: 5
                    }, {
                        label: '完成值',
                        data: [95, 110, 98, 85, 120, 92],
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
                            text: '备考核心指标完成率',
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

        // 备考模块占比图表
        const sectorCtx = document.getElementById('sectorChart')?.getContext('2d');
        if (sectorCtx) {
            new Chart(sectorCtx, {
                type: 'doughnut',
                data: {
                    labels: ['教育综合知识', '专业学科知识', '面试准备', '模拟练习', '错题复盘'],
                    datasets: [{
                        data: [35, 30, 15, 12, 8],
                        backgroundColor: [
                            'rgba(255, 193, 7, 0.7)',
                            'rgba(0, 123, 255, 0.7)',
                            'rgba(40, 167, 69, 0.7)',
                            'rgba(220, 53, 69, 0.7)',
                            'rgba(108, 117, 125, 0.7)'
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
                            text: '备考时间分配占比',
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

        // 增长趋势图表
        const growthCtx = document.getElementById('growthChart')?.getContext('2d');
        if (growthCtx) {
            new Chart(growthCtx, {
                type: 'line',
                data: {
                    labels: ['1月', '2月', '3月', '4月', '5月'],
                    datasets: [{
                        label: '模拟考试分数',
                        data: [65, 72, 80, 88, 92],
                        borderColor: '#ffc107',
                        backgroundColor: 'rgba(25
