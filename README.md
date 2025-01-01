<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audify</title>
    <link rel="icon" href="{{ url_for('static', filename='logo1.png') }}" type="image/png">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/aos/2.3.4/aos.css" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background: linear-gradient(135deg, #000000, #1a2f1a, #000000);
            color: #ffffff;
            line-height: 1.6;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(0, 0, 0, 0.9);
            padding: 20px 0;
            z-index: 1000;
            backdrop-filter: blur(10px);
        }

        .nav-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .nav-logo {
            font-size: 1.5rem;
            color: #2ee59d;
            text-decoration: none;
            font-weight: bold;
            letter-spacing: 1px;
        }

        .nav-links {
            display: flex;
            gap: 30px;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            transition: color 0.3s ease;
            font-weight: 500;
        }

        .nav-links a:hover {
            color: #2ee59d;
        }

        header {
            text-align: center;
            padding: 160px 0 60px;
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.3)),
                        url('/api/placeholder/1200/600') center/cover;
            margin-bottom: 60px;
            border-radius: 0 0 30px 30px;
        }

        h1 {
            font-size: 4.5rem;
            margin-bottom: 20px;
            text-shadow: 0 0 20px rgba(46, 229, 157, 0.5);
            letter-spacing: 2px;
        }

        .tagline {
            font-size: 1.8rem;
            color: #2ee59d;
            margin-bottom: 40px;
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
            margin: 60px 0;
        }

        .feature-card {
            background: rgba(0, 0, 0, 0.5);
            padding: 30px;
            border-radius: 15px;
            border: 1px solid #2ee59d;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, transparent, rgba(46, 229, 157, 0.1));
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(46, 229, 157, 0.15);
        }

        .feature-card:hover::before {
            opacity: 1;
        }

        .feature-card h3 {
            color: #2ee59d;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }

        .statistics {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin: 80px 0;
            text-align: center;
        }

        .stat-item {
            padding: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            transition: transform 0.3s ease;
        }

        .stat-item:hover {
            transform: translateY(-5px);
        }

        .stat-number {
            font-size: 3rem;
            color: #2ee59d;
            margin-bottom: 10px;
            font-weight: bold;
        }

        .free-banner {
            background: linear-gradient(90deg, #2ee59d, #26bc82);
            color: #000;
            padding: 20px;
            text-align: center;
            font-size: 1.8rem;
            font-weight: bold;
            margin: 40px 0;
            border-radius: 15px;
            animation: pulse 2s infinite;
            text-shadow: 0 1px 2px rgba(255, 255, 255, 0.3);
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        .testimonials {
            margin: 80px 0;
        }

        .testimonial-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .testimonial-card {
            background: rgba(0, 0, 0, 0.5);
            padding: 30px;
            border-radius: 15px;
            border: 1px solid rgba(46, 229, 157, 0.2);
            transition: transform 0.3s ease;
        }

        .testimonial-card:hover {
            transform: translateY(-5px);
            border-color: #2ee59d;
        }

        .testimonial-text {
            font-style: italic;
            margin-bottom: 20px;
            color: #e0e0e0;
        }

        .testimonial-author {
            color: #2ee59d;
            font-weight: bold;
        }

        .download-section {
            text-align: center;
            margin: 60px 0;
            padding: 60px 0;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 20px;
            border: 1px solid rgba(46, 229, 157, 0.2);
        }

        .download-section h2 {
            font-size: 2.5rem;
            margin-bottom: 40px;
            color: #2ee59d;
        }

        .download-buttons {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .download-btn {
            padding: 20px 40px;
            background: #2ee59d;
            color: #000000;
            text-decoration: none;
            border-radius: 30px;
            font-weight: bold;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            min-width: 250px;
            justify-content: center;
            font-size: 1.1rem;
            box-shadow: 0 5px 15px rgba(46, 229, 157, 0.3);
        }

        .download-btn svg {
            width: 24px;
            height: 24px;
        }

        .download-btn:hover {
            background: #ffffff;
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(46, 229, 157, 0.4);
        }

        footer {
            text-align: center;
            padding: 40px 0;
            margin-top: 60px;
            border-top: 1px solid rgba(46, 229, 157, 0.3);
            background: rgba(0, 0, 0, 0.8);
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 20px 0;
        }

        .social-links a {
            color: white;
            text-decoration: none;
            transition: color 0.3s ease;
            font-size: 1.1rem;
        }

        .social-links a:hover {
            color: #2ee59d;
        }

        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .tagline {
                font-size: 1.2rem;
            }

            .free-banner {
                font-size: 1.3rem;
                padding: 15px;
            }

            .download-btn {
                min-width: 200px;
                padding: 15px 30px;
            }
        }
    </style>
</head>
<body>
    <nav>
        <div class="nav-content">
            <a href="#" class="nav-logo">Audify</a>
            <div class="nav-links">
                <a href="#features">Features</a>
                <a href="#testimonials">Testimonials</a>
                <a href="#download">Download</a>
            </div>
        </div>
    </nav>

    <div class="container">
        <header>
            <h1 data-aos="fade-down">Audify</h1>
            <p class="tagline" data-aos="fade-up">Free Music For Everyone</p>
        </header>

        <div class="free-banner" data-aos="fade-up">
            100% FREE - No Premium, No Subscriptions, No Ads!
        </div>

        <section id="features" class="features">
            <div class="feature-card" data-aos="fade-up">
                <h3>Unlimited Downloads</h3>
                <p>Download your favorite tracks and enjoy them offline. No restrictions, no limits - just pure music enjoyment.</p>
            </div>

            <div class="feature-card" data-aos="fade-up" data-aos-delay="100">
                <h3>High Quality Audio</h3>
                <p>Experience crystal-clear sound quality with our premium audio streaming technology up to 320kbps.</p>
            </div>

            <div class="feature-card" data-aos="fade-up" data-aos-delay="200">
                <h3>Smart Playlists</h3>
                <p>Create and customize your playlists with our intelligent recommendation system.</p>
            </div>

            <div class="feature-card" data-aos="fade-up">
                <h3>Cross-Platform Sync</h3>
                <p>Seamlessly switch between devices while enjoying your favorite tunes with instant sync.</p>
            </div>

            <div class="feature-card" data-aos="fade-up" data-aos-delay="100">
                <h3>Zero Ads</h3>
                <p>Enjoy uninterrupted music streaming without any advertisements or interruptions.</p>
            </div>

            <div class="feature-card" data-aos="fade-up" data-aos-delay="200">
                <h3>Offline Mode</h3>
                <p>Access your downloaded music anywhere, anytime - even without an internet connection.</p>
            </div>
        </section>

        <section class="statistics">
            <div class="stat-item" data-aos="fade-up">
                <div class="stat-number">50M+</div>
                <p>Free Downloads</p>
            </div>
            <div class="stat-item" data-aos="fade-up" data-aos-delay="100">
                <div class="stat-number">100M+</div>
                <p>Available Songs</p>
            </div>
            <div class="stat-item" data-aos="fade-up" data-aos-delay="200">
                <div class="stat-number">190+</div>
                <p>Countries Served</p>
            </div>
        </section>

        <section id="testimonials" class="testimonials">
            <div class="testimonial-grid">
                <div class="testimonial-card" data-aos="fade-up">
                    <p class="testimonial-text">"Can't believe this is completely free! The download feature is amazing!"</p>
                    <p class="testimonial-author">- Sarah J.</p>
                </div>
                <div class="testimonial-card" data-aos="fade-up" data-aos-delay="100">
                    <p class="testimonial-text">"Best free music app ever. The sound quality is incredible!"</p>
                    <p class="testimonial-author">- Mike R.</p>
                </div>
                <div class="testimonial-card" data-aos="fade-up" data-aos-delay="200">
                    <p class="testimonial-text">"No ads, no subscriptions, just pure music. Perfect!"</p>
                    <p class="testimonial-author">- Lisa M.</p>
                </div>
            </div>
        </section>

        <section id="download" class="download-section" data-aos="fade-up">
            <h2>Download Audify Now</h2>
            <div class="download-buttons">
                <a href="#" class="download-btn">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
                        <line x1="8" y1="21" x2="16" y2="21"></line>
                        <line x1="12" y1="17" x2="12" y2="21"></line>
                    </svg>
                    Download for Windows
                </a>
                <a href="#" class="download-btn">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <polygon points="5 3 19 12 5 21 5 3"></polygon>
                    </svg>
                    Get it on Play Store
                    </a>
                    </div>
                </section>
        
                <footer>
                    <div class="social-links">
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
                            </svg>
                            Facebook
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-18 11.6 2.2.1 4.4-.6 6-2C3 15.5.5 9.6 3 5c2.2 2.6 5.6 4.1 9 4-.9-4.2 4-6.6 7-3.8 1.1 0 3-1.2 3-1.2z"></path>
                            </svg>
                            Twitter
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                            </svg>
                            Instagram
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M22.54 6.42a2.78 2.78 0 0 0-1.94-2C18.88 4 12 4 12 4s-6.88 0-8.6.46a2.78 2.78 0 0 0-1.94 2A29 29 0 0 0 1 11.75a29 29 0 0 0 .46 5.33A2.78 2.78 0 0 0 3.4 19c1.72.46 8.6.46 8.6.46s6.88 0 8.6-.46a2.78 2.78 0 0 0 1.94-2 29 29 0 0 0 .46-5.25 29 29 0 0 0-.46-5.33z"></path>
                                <polygon points="9.75 15.02 15.5 11.75 9.75 8.48 9.75 15.02"></polygon>
                            </svg>
                            YouTube
                        </a>
                    </div>
                    <p>&copy; 2025 Audify. All rights reserved.</p>
                </footer>
            </div>
        
            <script src="https://cdnjs.cloudflare.com/ajax/libs/aos/2.3.4/aos.js"></script>
            <script>
                AOS.init({
                    duration: 1000,
                    once: true,
                    offset: 100
                });
            </script>
        </body>
        </html>
