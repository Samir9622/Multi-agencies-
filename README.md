<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multi Agency Platform</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #3b82f6;
            --secondary-color: #10b981;
            --accent-color: #f59e0b;
            --dark-color: #1f2937;
            --light-color: #f3f4f6;
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 10px;
        }
        
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--primary-color);
            border-radius: 5px;
        }
        
        /* Smooth Scroll */
        html {
            scroll-behavior: smooth;
        }
        
        /* Animations */
        .fade-in {
            animation: fadeIn 0.8s ease-in-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .slide-in {
            animation: slideIn 0.8s ease-in-out;
        }
        
        @keyframes slideIn {
            from { transform: translateX(-50px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        
        /* Custom Components */
        .agency-card {
            transition: all 0.3s ease;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .agency-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 15px rgba(0,0,0,0.2);
        }
        
        .testimonial-card {
            transition: all 0.3s ease;
        }
        
        .testimonial-card:hover {
            transform: scale(1.03);
        }
        
        /* Custom Button */
        .custom-btn {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 12px 24px;
            border-radius: 50px;
            transition: all 0.3s ease;
            display: inline-block;
            text-decoration: none;
            text-align: center;
            font-weight: 600;
        }
        
        .custom-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        /* Service Tabs */
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease-in-out;
        }
        
        .tab {
            cursor: pointer;
            padding: 10px 20px;
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
        }
        
        .tab.active {
            border-bottom: 3px solid var(--primary-color);
            color: var(--primary-color);
            font-weight: 600;
        }
        
        /* Loader */
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--primary-color);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Custom Tooltip */
        .tooltip {
            position: relative;
            display: inline-block;
        }
        
        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background-color: var(--dark-color);
            color: white;
            text-align: center;
            border-radius: 6px;
            padding: 10px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        
        /* Mobile Menu */
        .mobile-menu {
            position: fixed;
            top: 0;
            right: -300px;
            width: 300px;
            height: 100vh;
            background-color: var(--dark-color);
            z-index: 1000;
            transition: all 0.3s ease-in-out;
            padding: 20px;
        }
        
        .mobile-menu.active {
            right: 0;
        }
        
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 999;
            display: none;
        }
        
        .overlay.active {
            display: block;
        }
        
        /* Progress Bar */
        .progress-container {
            width: 100%;
            height: 8px;
            background: #f1f1f1;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            width: 0%;
            transition: width 0.5s ease;
        }
        
        /* Sticky Header */
        .sticky-header {
            position: fixed;
            top: -100px;
            width: 100%;
            z-index: 998;
            transition: top 0.3s ease-in-out;
            background-color: white;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .sticky-header.active {
            top: 0;
        }
        
        /* Floating Contact Button */
        .float-contact {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background-color: var(--primary-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            z-index: 99;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .float-contact:hover {
            transform: scale(1.1);
            background-color: var(--secondary-color);
        }
        
        /* Dark Mode Toggle */
        .dark-mode {
            background-color: var(--dark-color) !important;
            color: var(--light-color) !important;
        }
        
        .dark-mode-toggle {
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .dark-mode-toggle:hover {
            transform: rotate(30deg);
        }
        
        /* Custom Contact Form */
        .form-input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 5px;
            border: 1px solid #e2e8f0;
            transition: all 0.3s ease;
            margin-bottom: 15px;
        }
        
        .form-input:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
            outline: none;
        }
        
        .form-error {
            color: #e53e3e;
            font-size: 14px;
            margin-top: -10px;
            margin-bottom: 10px;
            display: none;
        }
    </style>
</head>
<body class="font-sans">
    <!-- Header -->
    <header class="bg-white shadow-md py-4">
        <div class="container mx-auto px-4 md:px-6 flex justify-between items-center">
            <div class="flex items-center">
                <div class="text-2xl font-bold text-blue-600">
                    <span class="text-green-500">Multi</span>Agency
                </div>
            </div>
            
            <nav class="hidden md:flex space-x-8">
                <a href="#home" class="text-gray-700 hover:text-blue-600 transition-colors">Home</a>
                <div class="relative group">
                    <a href="#agencies" class="text-gray-700 hover:text-blue-600 transition-colors">Agencies</a>
                    <div class="absolute left-0 mt-2 w-48 bg-white shadow-lg rounded-md p-2 hidden group-hover:block z-10">
                        <a href="#travel" class="block px-4 py-2 text-gray-700 hover:bg-blue-100 rounded-md">Travel Agency</a>
                        <a href="#real-estate" class="block px-4 py-2 text-gray-700 hover:bg-blue-100 rounded-md">Real Estate</a>
                        <a href="#insurance" class="block px-4 py-2 text-gray-700 hover:bg-blue-100 rounded-md">Insurance</a>
                        <a href="#marketing" class="block px-4 py-2 text-gray-700 hover:bg-blue-100 rounded-md">Marketing</a>
                    </div>
                </div>
                <a href="#services" class="text-gray-700 hover:text-blue-600 transition-colors">Services</a>
                <a href="#testimonials" class="text-gray-700 hover:text-blue-600 transition-colors">Testimonials</a>
                <a href="#about" class="text-gray-700 hover:text-blue-600 transition-colors">About</a>
                <a href="#contact" class="text-gray-700 hover:text-blue-600 transition-colors">Contact</a>
            </nav>
            
            <div class="flex items-center space-x-4">
                <div class="dark-mode-toggle hidden md:block">
                    <i class="fas fa-moon text-gray-700 text-xl"></i>
                </div>
                <a href="#login" class="hidden md:block custom-btn">Login / Register</a>
                <div class="md:hidden hamburger-menu cursor-pointer">
                    <i class="fas fa-bars text-gray-700 text-2xl"></i>
                </div>
            </div>
        </div>
    </header>
    
    <!-- Sticky Header (appears on scroll) -->
    <header class="sticky-header">
        <div class="container mx-auto px-4 md:px-6 py-3 flex justify-between items-center">
            <div class="text-xl font-bold text-blue-600">
                <span class="text-green-500">Multi</span>Agency
            </div>
            
            <nav class="hidden md:flex space-x-6">
                <a href="#home" class="text-gray-700 hover:text-blue-600 transition-colors">Home</a>
                <a href="#agencies" class="text-gray-700 hover:text-blue-600 transition-colors">Agencies</a>
                <a href="#services" class="text-gray-700 hover:text-blue-600 transition-colors">Services</a>
                <a href="#contact" class="text-gray-700 hover:text-blue-600 transition-colors">Contact</a>
            </nav>
            
            <div class="flex items-center">
                <a href="#login" class="hidden md:block custom-btn text-sm py-2 px-4">Login</a>
                <div class="md:hidden hamburger-menu cursor-pointer">
                    <i class="fas fa-bars text-gray-700 text-2xl"></i>
                </div>
            </div>
        </div>
    </header>
    
    <!-- Mobile Menu -->
    <div class="overlay"></div>
    <div class="mobile-menu">
        <div class="flex justify-between items-center mb-8">
            <div class="text-xl font-bold text-white">
                <span class="text-green-400">Multi</span>Agency
            </div>
            <div class="close-menu cursor-pointer">
                <i class="fas fa-times text-white text-2xl"></i>
            </div>
        </div>
        
        <nav class="flex flex-col space-y-4">
            <a href="#home" class="text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">Home</a>
            
            <div class="mobile-dropdown">
                <div class="flex justify-between items-center text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">
                    <span>Agencies</span>
                    <i class="fas fa-chevron-down"></i>
                </div>
                <div class="mobile-dropdown-content hidden pl-4 mt-2 space-y-2">
                    <a href="#travel" class="block text-gray-300 hover:text-blue-300 py-2">Travel Agency</a>
                    <a href="#real-estate" class="block text-gray-300 hover:text-blue-300 py-2">Real Estate</a>
                    <a href="#insurance" class="block text-gray-300 hover:text-blue-300 py-2">Insurance</a>
                    <a href="#marketing" class="block text-gray-300 hover:text-blue-300 py-2">Marketing</a>
                </div>
            </div>
            
            <a href="#services" class="text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">Services</a>
            <a href="#testimonials" class="text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">Testimonials</a>
            <a href="#about" class="text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">About</a>
            <a href="#contact" class="text-white hover:text-blue-300 transition-colors py-2 border-b border-gray-700">Contact</a>
        </nav>
        
        <div class="mt-8">
            <a href="#login" class="block w-full custom-btn text-center">Login / Register</a>
        </div>
        
        <div class="mt-8 flex justify-center">
            <div class="dark-mode-toggle-mobile text-white">
                <i class="fas fa-moon text-xl"></i>
            </div>
        </div>
    </div>
    
    <!-- Hero Section -->
    <section id="home" class="py-20 bg-gradient-to-br from-blue-50 to-green-50">
        <div class="container mx-auto px-4 md:px-6">
            <div class="flex flex-col md:flex-row items-center">
                <div class="md:w-1/2 mb-10 md:mb-0 fade-in">
                    <h1 class="text-4xl md:text-5xl font-bold text-gray-800 mb-4">Your One-Stop <span class="text-blue-600">Multi-Agency</span> Platform</h1>
                    <p class="text-lg text-gray-600 mb-8">Access multiple agency services in one place - travel, real estate, insurance, and marketing solutions tailored to your needs.</p>
                    <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
                        <a href="#agencies" class="custom-btn">Explore Agencies</a>
                        <a href="#contact" class="bg-white text-blue-600 border-2 border-blue-600 hover:bg-blue-50 transition-colors py-3 px-6 rounded-full font-semibold text-center">Contact Us</a>
                    </div>
                </div>
                <div class="md:w-1/2 slide-in">
                    <div class="relative">
                        <div class="bg-blue-600 w-72 h-72 rounded-full absolute top-4 left-4 opacity-20"></div>
                        <div class="bg-green-600 w-72 h-72 rounded-full absolute top-0 left-0 opacity-20"></div>
                        <div class="relative bg-white p-6 rounded-xl shadow-xl">
                            <div class="grid grid-cols-2 gap-4">
                                <div class="bg-blue-50 p-4 rounded-lg">
                                    <i class="fas fa-plane-departure text-3xl text-blue-600 mb-2"></i>
                                    <h3 class="font-bold text-gray-800">Travel</h3>
                                    <p class="text-sm text-gray-600">Book flights, hotels & packages</p>
                                </div>
                                <div class="bg-green-50 p-4 rounded-lg">
                                    <i class="fas fa-home text-3xl text-green-600 mb-2"></i>
                                    <h3 class="font-bold text-gray-800">Real Estate</h3>
                                    <p class="text-sm text-gray-600">Find property & consultation</p>
                                </div>
                                <div class="bg-yellow-50 p-4 rounded-lg">
                                    <i class="fas fa-shield-alt text-3xl text-yellow-600 mb-2"></i>
                                    <h3 class="font-bold text-gray-800">Insurance</h3>
                                    <p class="text-sm text-gray-600">Protect what matters most</p>
                                </div>
                                <div class="bg-purple-50 p-4 rounded-lg">
                                    <i class="fas fa-bullhorn text-3xl text-purple-600 mb-2"></i>
                                    <h3 class="font-bold text-gray-800">Marketing</h3>
                                    <p class="text-sm text-gray-600">Grow your business</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Statistics -->
    <section class="py-16 bg-white">
        <div class="container mx-auto px-4 md:px-6">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
                <div class="text-center">
                    <div class="text-4xl font-bold text-blue-600 mb-2 counter" data-target="500">0</div>
                    <p class="text-gray-600">Agencies</p>
                </div>
                <div class="text-center">
                    <div class="text-4xl font-bold text-green-600 mb-2 counter" data-target="10000">0</div>
                    <p class="text-gray-600">Clients Served</p>
                </div>
                <div class="text-center">
                    <div class="text-4xl font-bold text-yellow-600 mb-2 counter" data-target="50">0</div>
                    <p class="text-gray-600">Countries</p>
                </div>
                <div class="text-center">
                    <div class="text-4xl font-bold text-purple-600 mb-2 counter" data-target="95">0</div>
                    <p class="text-gray-600">Satisfaction Rate</p>
                    <span class="text-lg">%</span>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Agency Sectors -->
    <section id="agencies" class="py-20 bg-gray-100">
        <div class="container mx-auto px-4 md:px-6">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-4">Our Agency Sectors</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">Discover our diverse range of agency services that cater to all your personal and business needs.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Travel Agency -->
                <div id="travel" class="agency-card bg-white">
                    <div class="h-48 bg-blue-600 flex items-center justify-center">
                        <i class="fas fa-plane text-white text-5xl"></i>
                    </div>
                    <div class="p-6">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Travel Agency</h3>
                        <p class="text-gray-600 mb-4">Book flights, hotels, packages and tours worldwide with our premium travel services.</p>
                        <div class="flex justify-between items-center">
                            <a href="#" class="text-blue-600 hover:text-blue-800 font-semibold" id="travel-details">Learn More</a>
                            <i class="fas fa-arrow-right text-blue-600"></i>
                        </div>
                    </div>
                </div>
                
                <!-- Real Estate -->
                <div id="real-estate" class="agency-card bg-white">
                    <div class="h-48 bg-green-600 flex items-center justify-center">
                    
