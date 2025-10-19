<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NextGen Mobile Shop - Catalogue</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            /* Using a very light off-white background for subtle texture */
            background-color: #fcfcfd; 
        }
        /* Custom scrollbar for aesthetic purposes */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-thumb {
            background: #a78bfa; /* purple-400 */
            border-radius: 10px;
        }
        .product-card {
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 25px -5px rgba(109, 40, 217, 0.2), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* Enhanced shadow with purple tint */
        }
        .modal-overlay {
            background-color: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(5px); /* Added subtle blur for focus */
        }
        /* Spinning animation for loader */
        @keyframes spin {
          0% { transform: rotate(0deg); }
          100% { transform: rotate(360deg); }
        }
        .spinner {
          border: 4px solid rgba(255, 255, 255, 0.3);
          border-top: 4px solid #fff;
          border-radius: 50%;
          width: 30px;
          height: 30px;
          animation: spin 1s linear infinite;
        }
        /* Custom slow pulse animation for hero element */
        @keyframes pulse-slow {
          0%, 100% { transform: scale(1); opacity: 0.9; }
          50% { transform: scale(1.05); opacity: 1; }
        }
        .animate-pulse-slow {
            animation: pulse-slow 4s infinite ease-in-out;
        }
    </style>
</head>
<body class="antialiased text-gray-800">

    <!-- Header & Navigation -->
    <header class="bg-white shadow-lg sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex justify-between items-center">
            <!-- Logo -->
            <a href="#" class="flex items-center space-x-2 text-2xl font-bold text-indigo-600">
                <i data-lucide="smartphone" class="w-6 h-6"></i>
                <span>NextGen Mobiles Catalogue</span>
            </a>

            <!-- Navigation Links (Hidden on Mobile, Visible on Desktop) -->
            <nav class="hidden md:flex space-x-6 text-gray-600 font-medium">
                <a href="#" class="hover:text-indigo-600 transition duration-150">Home</a>
                <a href="#" class="hover:text-indigo-600 transition duration-150">Catalogue</a>
                <a href="#" class="hover:text-indigo-600 transition duration-150">About Us</a>
                <a href="#" class="hover:text-indigo-600 transition duration-150">Contact</a>
            </nav>

            <!-- Actions (Simplified - only user profile remains) -->
            <div class="flex items-center space-x-4">
                <button class="p-2 rounded-full bg-gray-100 text-gray-600 hover:bg-gray-200 transition duration-150">
                    <i data-lucide="user" class="w-5 h-5"></i>
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-10 pb-20">
        
        <!-- Hero Section / Banner - Updated with a Gradient Background -->
        <section class="bg-gradient-to-r from-indigo-700 to-purple-600 text-white rounded-xl p-8 md:p-16 mb-12 shadow-2xl overflow-hidden relative flex flex-col md:flex-row items-center justify-between">
            <div class="max-w-xl mb-8 md:mb-0 relative z-10">
                <!-- NEW H1 -->
                <h1 class="text-4xl md:text-5xl font-extrabold mb-4 leading-tight">
                    The Future is Mobile: Next-Gen Devices in BDT
                </h1>
                <!-- NEW P -->
                <p class="text-indigo-200 text-lg mb-6">
                    Explore a curated selection of flagship and budget smartphones from top global brands like Apple, Samsung, Vivo, and Tecno. Use our real-time filters to find your perfect phone at the right price.
                </p>
                <!-- Updated Button Color -->
                <button class="bg-white text-purple-600 font-bold py-3 px-6 rounded-full hover:bg-gray-100/90 transition duration-300 shadow-lg flex items-center space-x-2">
                    <i data-lucide="search" class="w-5 h-5"></i>
                    <span>Browse Full Specs</span>
                </button>
            </div>
            <!-- Dynamic, Pulsing Background Visual (More Attractive) -->
            <div class="w-48 h-48 md:w-64 md:h-64 bg-purple-500/30 backdrop-blur-sm rounded-full flex items-center justify-center shadow-2xl border-4 border-white/50 animate-pulse-slow relative z-0">
                 <i data-lucide="zap" class="w-28 h-28 text-white"></i>
            </div>
        </section>

        <!-- --- Price & Brand Filter Section --- -->
        <section class="mb-10 bg-white p-6 rounded-xl shadow-md border border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 mb-4 flex items-center space-x-2">
                <i data-lucide="sliders" class="w-5 h-5 text-indigo-500"></i>
                <span>Customize Your Search</span>
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4 items-end">
                
                <!-- Brand Filter (NEW) -->
                <div class="col-span-1">
                    <label for="brand-filter" class="block text-sm font-medium text-gray-700 mb-1">Select Brand</label>
                    <select id="brand-filter" onchange="filterProducts()" class="w-full p-2.5 border border-gray-300 rounded-lg bg-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150">
                        <!-- Options injected by JS -->
                    </select>
                </div>

                <!-- Min Price Input -->
                <div class="col-span-1">
                    <label for="min-price" class="block text-sm font-medium text-gray-700 mb-1">Min Price (৳)</label>
                    <input type="number" id="min-price" oninput="filterProducts()" placeholder="e.g., 10000" class="w-full p-2 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500 transition duration-150" min="0">
                </div>
                <!-- Max Price Input -->
                <div class="col-span-1">
                    <label for="max-price" class="block text-sm font-medium text-gray-700 mb-1">Max Price (৳)</label>
                    <input type="number" id="max-price" oninput="filterProducts()" placeholder="e.g., 50000" class="w-full p-2 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500 transition duration-150" min="0">
                </div>
                
                <!-- Quick Filter Buttons -->
                <div class="col-span-2 flex flex-wrap gap-2">
                    <button onclick="setQuickFilter(10000, 30000)" class="px-3 py-2 text-sm rounded-full bg-indigo-50 hover:bg-indigo-100 text-indigo-700 font-medium transition whitespace-nowrap">৳10k - 30k (Budget)</button>
                    <button onclick="setQuickFilter(50000, 90000)" class="px-3 py-2 text-sm rounded-full bg-indigo-50 hover:bg-indigo-100 text-indigo-700 font-medium transition whitespace-nowrap">৳50k - 90k (Mid)</button>
                    <button onclick="setQuickFilter(100000, 200000)" class="px-3 py-2 text-sm rounded-full bg-indigo-50 hover:bg-indigo-100 text-indigo-700 font-medium transition whitespace-nowrap">৳100k+ (Flagship)</button>
                    <button onclick="clearFilter()" class="px-3 py-2 text-sm rounded-full bg-red-50 hover:bg-red-100 text-red-700 font-medium transition flex items-center whitespace-nowrap">
                        <i data-lucide="x-circle" class="w-4 h-4 mr-1"></i>
                        Clear Filters
                    </button>
                </div>
            </div>
            <p id="filter-message" class="text-sm text-red-600 mt-2 hidden flex items-center">
                <i data-lucide="bell" class="w-4 h-4 mr-1"></i>
                Please ensure the minimum price is less than the maximum price.
            </p>
        </section>
        <!-- ----------------------------------------- -->

        <!-- Product Catalogue Section -->
        <section>
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center md:text-left">Featured Devices (Prices in ৳ BDT)</h2>
            
            <!-- Product Grid -->
            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Products will be injected here by JavaScript -->
            </div>
            
            <!-- No Results Message -->
            <div id="no-results" class="hidden text-center py-12">
                <i data-lucide="frown" class="w-12 h-12 mx-auto text-gray-400 mb-4"></i>
                <p class="text-xl text-gray-600">Sorry, no products match your current budget and brand selection.</p>
                <button onclick="clearFilter()" class="mt-4 text-indigo-600 hover:text-indigo-800 font-medium flex items-center justify-center mx-auto">
                    <i data-lucide="refresh-cw" class="w-4 h-4 mr-1"></i>
                    Clear Filters to see all devices
                </button>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-10 mt-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-2 md:grid-cols-4 gap-8">
            <div>
                <h3 class="font-bold text-lg mb-3 text-indigo-400">Company</h3>
                <ul class="space-y-2 text-gray-400 text-sm">
                    <li><a href="#" class="hover:text-white transition duration-150">Our Story</a></li>
                    <li><a href="#" class="hover:text-white transition duration-150">Careers</a></li>
                    <li><a href="#" class="hover:text-white transition duration-150">Press</a></li>
                </ul>
            </div>
            <!-- UPDATED: Contact & Support Section -->
            <div>
                <h3 class="font-bold text-lg mb-3 text-indigo-400">Contact & Support</h3>
                <ul class="space-y-2 text-gray-400 text-sm">
                    <!-- Email Address -->
                    <li>
                        <a href="mailto:shihabmdzubayersalehin@gmail.com" class="hover:text-white transition duration-150 flex items-center">
                            <i data-lucide="mail" class="w-4 h-4 mr-2"></i> 
                            shihabmdzubayersalehin@gmail.com
                        </a>
                    </li>
                    <!-- Phone Number -->
                    <li>
                        <a href="tel:+8801330797876" class="hover:text-white transition duration-150 flex items-center">
                            <i data-lucide="phone" class="w-4 h-4 mr-2"></i> 
                            01330797876
                        </a>
                    </li>
                    <li><a href="#" class="hover:text-white transition duration-150">FAQ</a></li>
                    <li><a href="#" class="hover:text-white transition duration-150">Shipping & Returns</a></li>
                </ul>
            </div>
            <div>
                <h3 class="font-bold text-lg mb-3 text-indigo-400">Legal</h3>
                <ul class="space-y-2 text-gray-400 text-sm">
                    <li><a href="#" class="hover:text-white transition duration-150">Privacy Policy</a></li>
                    <li><a href="#" class="hover:text-white transition duration-150">Terms of Service</a></li>
                </ul>
            </div>
            <div class="col-span-2 md:col-span-1">
                <h3 class="font-bold text-lg mb-3 text-indigo-400">Newsletter</h3>
                <p class="text-gray-400 text-sm mb-4">
                    Get the latest releases and news updates.
                </p>
                <div class="flex">
                    <input type="email" placeholder="Your email" class="p-3 rounded-l-lg text-gray-900 focus:outline-none w-full">
                    <button class="bg-indigo-600 p-3 rounded-r-lg hover:bg-indigo-700 transition duration-150">
                        <i data-lucide="send" class="w-5 h-5"></i>
                    </button>
                </div>
            </div>
        </div>
        <div class="border-t border-gray-700 mt-8 pt-6 text-center text-gray-500 text-sm">
            &copy; 2025 NextGen Mobile Catalogue. All rights reserved.
        </div>
    </footer>

    <!-- Product Detail Modal (Hidden by default) -->
    <div id="product-modal" class="hidden fixed inset-0 z-[100] flex items-center justify-center p-4 modal-overlay" onclick="closeModal(event)">
        <div id="modal-content-card" class="bg-white rounded-xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-y-auto transform transition-all duration-300 scale-95 opacity-0" onclick="event.stopPropagation()">
            <div class="p-6 md:p-8 flex flex-col md:flex-row space-y-6 md:space-y-0 md:space-x-8">
                
                <!-- Close Button -->
                <button class="absolute top-4 right-4 text-gray-500 hover:text-gray-900 transition duration-150" onclick="closeModal()">
                    <i data-lucide="x" class="w-6 h-6"></i>
                </button>

                <!-- Product Image Area -->
                <div class="md:w-1/2 flex items-center justify-center bg-gray-100 rounded-lg p-6">
                    <img id="modal-image" src="" alt="Product Image" class="w-full h-auto max-h-80 object-contain rounded-lg">
                </div>

                <!-- Product Info Area -->
                <div class="md:w-1/2">
                    <h2 id="modal-name" class="text-3xl font-bold text-gray-900 mb-2"></h2>
                    <p class="text-indigo-600 text-2xl font-extrabold mb-6">
                        Price: ৳<span id="modal-price"></span>
                    </p>
                    
                    <h3 class="text-lg font-semibold mb-2">Detailed Overview</h3>
                    <p id="modal-description" class="text-gray-600 mb-6 leading-relaxed"></p>

                    <div class="space-y-4">
                        <h3 class="text-lg font-semibold mb-2">Key Specifications</h3>
                        <!-- Key Features / Specs List -->
                        <ul id="modal-specs-list" class="space-y-2 text-gray-700">
                            <!-- Specs will be injected here by JS -->
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Initialize Lucide Icons
        lucide.createIcons();

        // --- Product Data (Expanded List including Tecno and Infinix) ---
        const products = [
            // --- APPLE (Flagship & Mid-range) ---
            { 
                id: 1, 
                name: "iPhone 18 Pro Max", 
                price: 195000, 
                brand: "Apple",
                desc: "Powerful A18 Bionic chip, cinematic video, and ProMotion display. Unmatched performance and ecosystem experience.", 
                image: "https://placehold.co/400x400/1D4ED8/ffffff?text=Loading", 
                imagePrompt: "Minimalist black smartphone with triple camera system, large screen, sleek design, on a white background, studio quality, product photo",
                specs: {
                    Display: ["6.7-inch Super Retina XDR OLED", "ProMotion 120Hz Technology", "Ceramic Shield Front Cover"],
                    Camera: ["Main: 48MP (Sensor-shift OIS)", "Telephoto: 12MP (5x Optical Zoom)"],
                    Platform: ["Apple A18 Bionic Chip", "6GB RAM (estimated)"],
                    Battery: ["Estimated 4800mAh Battery", "15W MagSafe Wireless Charging"]
                }
            },
            { 
                id: 11, 
                name: "iPhone 16", 
                price: 155000, 
                brand: "Apple",
                desc: "The latest main-line iPhone. Excellent dual-camera system, robust design, and all-day battery life.", 
                image: "https://placehold.co/400x400/3B82F6/ffffff?text=Loading", 
                imagePrompt: "Standard blue iPhone, dual camera setup, high quality product shot, simple background",
                specs: {
                    Display: ["6.1-inch Super Retina XDR OLED", "60Hz Standard Refresh Rate"],
                    Camera: ["Main: 48MP Wide (OIS)", "Ultra-wide: 12MP"],
                    Platform: ["Apple A17 Bionic Chip", "6GB RAM (estimated)"],
                    Battery: ["Estimated 4500mAh Battery", "20W Fast Charging"]
                }
            },
            { 
                id: 12, 
                name: "iPhone SE (4th Gen)", 
                price: 52000, 
                brand: "Apple",
                desc: "Flagship A-series power in a compact, classic design. Perfect for Apple fans on a budget.", 
                image: "https://placehold.co/400x400/10B981/ffffff?text=Loading", 
                imagePrompt: "White iPhone SE with large bezels, single camera, on a clean desk, affordable Apple look",
                specs: {
                    Display: ["4.7-inch Retina HD LCD", "Classic Home Button"],
                    Camera: ["Main: 12MP Single Lens (OIS)"],
                    Platform: ["Apple A15 Bionic Chip", "4GB RAM (estimated)"],
                    Battery: ["Estimated 2000mAh Battery", "18W Fast Charging"]
                }
            },

            // --- SAMSUNG (Flagship, Mid-range & Budget) ---
            { 
                id: 2, 
                name: "Samsung Galaxy S25 Ultra", 
                price: 169999, 
                brand: "Samsung",
                desc: "The ultimate flagship with a 200MP camera, S Pen support, and a stunning Dynamic AMOLED display.", 
                image: "https://placehold.co/400x400/0E7490/ffffff?text=Loading", 
                imagePrompt: "Ultra modern high-end smartphone with stylus and four cameras, titanium finish, on a white background, studio quality, product photo",
                specs: {
                    Display: ["6.8-inch Dynamic AMOLED 2X", "1-120Hz Adaptive Refresh Rate"],
                    Camera: ["Main: 200MP Wide (OIS)", "Periscope: 50MP (10x Optical)"],
                    Platform: ["Snapdragon 8 Gen 4 for Galaxy", "12GB RAM LPDDR5X"],
                    Battery: ["5000mAh Capacity", "45W Super Fast Charging"]
                }
            },
            { 
                id: 13, 
                name: "Samsung Galaxy A55", 
                price: 45999, 
                brand: "Samsung",
                desc: "Premium mid-range phone with a stunning Super AMOLED display, metal frame, and capable triple camera.", 
                image: "https://placehold.co/400x400/F59E0B/ffffff?text=Loading", 
                imagePrompt: "Mid-range Samsung Galaxy A-series phone, pastel blue color, triple camera system, clean shot",
                specs: {
                    Display: ["6.6-inch Super AMOLED", "120Hz Refresh Rate"],
                    Camera: ["Main: 50MP (OIS)", "Ultra-wide: 12MP", "Macro: 5MP"],
                    Platform: ["Exynos 1480", "8GB RAM"],
                    Battery: ["5000mAh Capacity", "25W Fast Charging"]
                }
            },
            { 
                id: 14, 
                name: "Samsung Galaxy M15", 
                price: 14999, 
                brand: "Samsung",
                desc: "Budget-friendly phone with a massive **6000mAh battery** and Super AMOLED display. Unmatched endurance.", 
                image: "https://placehold.co/400x400/8B5CF6/ffffff?text=Loading", 
                imagePrompt: "Budget Samsung Galaxy M-series phone, dark purple color, large battery capacity focus, product shot",
                specs: {
                    Display: ["6.5-inch Super AMOLED", "90Hz Refresh Rate"],
                    Camera: ["Main: 50MP", "Ultra-wide: 5MP"],
                    Platform: ["MediaTek Dimensity 6100+", "4GB RAM"],
                    Battery: ["6000mAh Capacity", "25W Fast Charging"]
                }
            },

            // --- VIVO (Flagship, Mid-range & Budget) ---
            { 
                id: 3, 
                name: "Vivo V30 Pro", 
                price: 68990, 
                brand: "Vivo",
                desc: "A flagship portrait phone with **ZEISS optics** and a stunning curved AMOLED display. Excellent camera performance.", 
                image: "https://placehold.co/400x400/0047AB/ffffff?text=Loading", 
                imagePrompt: "High-end Vivo smartphone, sleek black back, large camera module with ZEISS branding, studio lighting, product photo",
                specs: {
                    Display: ["6.78-inch AMOLED Curved Display", "120Hz Refresh Rate"],
                    Camera: ["Main: 50MP (ZEISS OIS)", "Telephoto: 50MP (2x Optical)"],
                    Platform: ["MediaTek Dimensity 8200", "12GB RAM LPDDR5X"],
                    Battery: ["4800mAh Capacity", "80W FlashCharge"]
                }
            },
            { 
                id: 15, 
                name: "Vivo X100 Pro", 
                price: 145000, 
                brand: "Vivo",
                desc: "The absolute pinnacle of mobile photography, featuring a 1-inch sensor and the latest V3 imaging chip.", 
                image: "https://placehold.co/400x400/EF4444/ffffff?text=Loading", 
                imagePrompt: "Ultra-flagship Vivo X-series phone, massive circular camera module, deep orange vegan leather finish, high-end studio shot",
                specs: {
                    Display: ["6.78-inch LTPO AMOLED", "120Hz Adaptive Refresh Rate"],
                    Camera: ["Main: 50MP (1-inch Sensor)", "Periscope: 50MP (4.3x Optical)", "V3 Imaging Chip"],
                    Platform: ["MediaTek Dimensity 9300", "16GB RAM LPDDR5X"],
                    Battery: ["5400mAh Capacity", "100W Wired, 50W Wireless Charging"]
                }
            },
            { 
                id: 16, 
                name: "Vivo Y200e", 
                price: 26990, 
                brand: "Vivo",
                desc: "Stylish and reliable mid-range device with a premium vegan leather finish and solid camera performance.", 
                image: "https://placehold.co/400x400/94A3B8/ffffff?text=Loading", 
                imagePrompt: "Budget Vivo Y-series phone, vegan leather texture on the back, dual camera setup, soft focus shot",
                specs: {
                    Display: ["6.67-inch AMOLED", "120Hz Refresh Rate"],
                    Camera: ["Main: 50MP (OIS)", "Depth: 2MP"],
                    Platform: ["Snapdragon 4 Gen 2", "6GB/8GB RAM"],
                    Battery: ["5000mAh Capacity", "44W Fast Charging"]
                }
            },

            // --- REALME (Mid-range & Budget) ---
            { 
                id: 4, 
                name: "Realme GT Neo 6", 
                price: 49990, 
                brand: "Realme",
                desc: "High-performance smartphone built for speed and fluid gaming with powerful processor and vibrant screen.", 
                image: "https://placehold.co/400x400/1F2937/ffffff?text=Loading", 
                imagePrompt: "High-performance smartphone with yellow accent or racing stripe on the back, futuristic tech background, gaming focus, product photo",
                specs: {
                    Display: ["6.7-inch Super AMOLED", "144Hz Variable Refresh Rate"],
                    Camera: ["Main: 50MP Wide (OIS)", "Ultra-wide: 8MP"],
                    Platform: ["Snapdragon 8+ Gen 1 Processor", "12GB/16GB RAM"],
                    Battery: ["5000mAh Dual-Cell Battery", "80W SuperDart Charge"]
                }
            },
            { 
                id: 17, 
                name: "Realme 13 Pro", 
                price: 58990, 
                brand: "Realme",
                desc: "Premium experience with a **curved display**, exceptional fast charging, and a beautiful design.", 
                image: "https://placehold.co/400x400/991B1B/ffffff?text=Loading", 
                imagePrompt: "Red colored upper mid-range Realme phone, curved display visible, high glossy finish, product photo",
                specs: {
                    Display: ["6.7-inch Curved AMOLED", "120Hz Refresh Rate"],
                    Camera: ["Main: 108MP ProLight", "Telephoto: 32MP (2x Optical)"],
                    Platform: ["MediaTek Dimensity 7050", "12GB RAM"],
                    Battery: ["5000mAh Capacity", "67W SuperVOOC Charge"]
                }
            },
            { 
                id: 5, 
                name: "Realme C65", 
                price: 16990, 
                brand: "Realme",
                desc: "An affordable champion offering smooth performance and premium design features for the budget-conscious user.", 
                image: "https://placehold.co/400x400/8B5CF6/ffffff?text=Loading", 
                imagePrompt: "Affordable budget smartphone, glossy purple finish, clean background, product photo",
                specs: {
                    Display: ["6.67-inch IPS LCD Display", "90Hz Refresh Rate"],
                    Camera: ["Main: 50MP AI Camera", "Front: 8MP"],
                    Platform: ["MediaTek Helio G85 Processor", "6GB RAM"],
                    Battery: ["5000mAh Capacity", "15W Charging Support"]
                }
            },

            // --- NOKIA (Mid-range & Budget) ---
            { 
                id: 6, 
                name: "Nokia C22", 
                price: 13500, 
                brand: "Nokia",
                desc: "The lowest-priced smartphone. Focused on durability and 3-day battery life. Essential features for first-time users.", 
                image: "https://placehold.co/400x400/F59E0B/ffffff?text=Loading", 
                imagePrompt: "Entry-level smartphone, focus on durability and solid build, dark gray color, close-up shot, product photo",
                specs: {
                    Display: ["6.5-inch HD+ Display", "Toughened Glass Protection"],
                    Camera: ["Main: 13MP", "Front: 8MP"],
                    Platform: ["Unisoc SC9863A Processor", "3GB/4GB RAM", "Android 13 Go Edition"],
                    Battery: ["5050mAh Capacity (3-Day Battery Life)", "IP52 Protection"]
                }
            },
            { 
                id: 18, 
                name: "Nokia G400 5G", 
                price: 32000, 
                brand: "Nokia",
                desc: "Reliable 5G mid-ranger with a durable design, near-stock Android experience, and high-refresh-rate display.", 
                image: "https://placehold.co/400x400/059669/ffffff?text=Loading", 
                imagePrompt: "Mid-range Nokia phone, forest green color, solid build quality, product shot",
                specs: {
                    Display: ["6.6-inch IPS LCD", "120Hz Refresh Rate"],
                    Camera: ["Main: 48MP", "Ultra-wide: 5MP"],
                    Platform: ["Snapdragon 480+ 5G", "6GB RAM"],
                    Battery: ["5000mAh Capacity", "20W Fast Charging"]
                }
            },
            // --- GOOGLE, ONEPLUS, MOTOROLA, XIAOMI ---
            { 
                id: 7, 
                name: "Google Pixel 10", 
                price: 85500, 
                brand: "Google",
                desc: "Pure Android experience with revolutionary AI features and the best computational photography in the market.", 
                image: "https://placehold.co/400x400/4F46E5/ffffff?text=Loading", 
                imagePrompt: "Modern dual-tone smartphone with a signature camera bar, on a clean, light background, high-angle shot, product photo",
                specs: {
                    Display: ["6.3-inch Actua OLED Display", "120Hz Refresh Rate"],
                    Camera: ["Main: 50MP Wide (OIS)", "Ultra-wide: 12MP"],
                    Platform: ["Google Tensor G4 Chip", "Titan M2 Security Coprocessor"],
                    Battery: ["4600mAh Capacity", "30W Fast Charging"]
                }
            },
            { 
                id: 8, 
                name: "OnePlus 13R", 
                price: 62900, 
                brand: "OnePlus",
                desc: "A performance beast with 100W SuperVOOC charging and a silky-smooth 120Hz Fluid AMOLED display.", 
                image: "https://placehold.co/400x400/991B1B/ffffff?text=Loading", 
                imagePrompt: "Red colored high-end gaming smartphone, sleek aesthetic, fast charge visual effect, on a dark background, product photo",
                specs: {
                    Display: ["6.74-inch Fluid AMOLED", "120Hz Adaptive Refresh Rate"],
                    Camera: ["Main: 64MP Wide (OIS)", "Ultra-wide: 8MP"],
                    Platform: ["MediaTek Dimensity 9200+", "16GB LPDDR5X RAM"],
                    Battery: ["5500mAh Capacity", "100W SUPERVOOC Charging"]
                }
            },
            { 
                id: 9, 
                name: "Xiaomi Redmi Note 14 Pro", 
                price: 34500, 
                brand: "Xiaomi",
                desc: "Best-value mid-ranger with a 108MP camera, long-lasting battery, and fast charging. The perfect balance of features and cost.", 
                image: "https://placehold.co/400x400/581C87/ffffff?text=Loading", 
                imagePrompt: "Mid-range smartphone, vibrant blue glossy back, large camera module, on a neutral grey studio surface, product photo",
                specs: {
                    Display: ["6.67-inch AMOLED DotDisplay", "120Hz Refresh Rate"],
                    Camera: ["Main: 108MP Wide", "Ultra-wide: 8MP"],
                    Platform: ["Snapdragon 778G+ 5G Processor", "8GB RAM"],
                    Battery: ["5000mAh Capacity", "67W Turbo Charging"]
                }
            },
            { 
                id: 10, 
                name: "Motorola Moto G50", 
                price: 19990, 
                brand: "Motorola",
                desc: "Budget-friendly 5G experience with a massive battery and clean, near-stock Android software. Reliable daily driver.", 
                image: "https://placehold.co/400x400/059669/ffffff?text=Loading", 
                imagePrompt: "Budget 5G Android smartphone, clean design, mint green color, simple shot on white background, product photo",
                specs: {
                    Display: ["6.5-inch Max Vision HD+", "90Hz Refresh Rate"],
                    Camera: ["Main: 48MP (Quad Pixel)", "Depth: 2MP"],
                    Platform: ["Snapdragon 480 5G Processor", "4GB RAM"],
                    Battery: ["6000mAh Capacity", "15W Charging Support"]
                }
            },
            
            // --- TECNO (NEW ADDITIONS) ---
            { 
                id: 19, 
                name: "Tecno Camon 30 Premier", 
                price: 64990, 
                brand: "Tecno",
                desc: "Premium experience with a dedicated imaging chip, advanced camera features, and large memory capacity.", 
                image: "https://placehold.co/400x400/FF00FF/ffffff?text=Loading", 
                imagePrompt: "High-end Tecno smartphone, black body, large circular camera module, professional product shot.",
                specs: {
                    Display: ["6.77-inch LTPO AMOLED", "120Hz Adaptive Refresh Rate"],
                    Camera: ["Main: 50MP (OIS)", "Periscope: 50MP (3x Optical)", "50MP Ultra-wide"],
                    Platform: ["MediaTek Dimensity 8200 Ultra", "12GB RAM"],
                    Battery: ["5000mAh Capacity", "70W Ultra Charge"]
                }
            },
            { 
                id: 20, 
                name: "Tecno Spark 20 Pro+", 
                price: 24990, 
                brand: "Tecno",
                desc: "Mid-range stylish device with a curved display, 108MP camera, and superior stereo speakers.", 
                image: "https://placehold.co/400x400/FF5733/ffffff?text=Loading", 
                imagePrompt: "Stylish mid-range Tecno phone, curved screen visible, gold or bronze color finish, product photo.",
                specs: {
                    Display: ["6.78-inch AMOLED Curved Display", "120Hz Refresh Rate"],
                    Camera: ["Main: 108MP Ultra Sensor", "Front: 32MP Selfie Camera"],
                    Platform: ["MediaTek Helio G99 Ultimate", "8GB RAM"],
                    Battery: ["5000mAh Capacity", "33W Fast Charging"]
                }
            },
            { 
                id: 21, 
                name: "Tecno Pop 8", 
                price: 11500, 
                brand: "Tecno",
                desc: "An entry-level smartphone focusing on long battery life and a large, bright display for daily tasks.", 
                image: "https://placehold.co/400x400/00FFFF/000000?text=Loading", 
                imagePrompt: "Simple, budget Tecno phone, plastic build, large size, dark blue color, focused on affordability.",
                specs: {
                    Display: ["6.6-inch HD+ LCD", "90Hz Refresh Rate"],
                    Camera: ["Main: 13MP Dual Camera"],
                    Platform: ["Unisoc T606", "4GB RAM"],
                    Battery: ["5000mAh Capacity", "10W Charging"]
                }
            },

            // --- INFINIX (NEW ADDITIONS) ---
            { 
                id: 22, 
                name: "Infinix GT 20 Pro", 
                price: 47990, 
                brand: "Infinix",
                desc: "Dedicated gaming phone with Cyberpunk-inspired design, specialized chip, and a 144Hz AMOLED display.", 
                image: "https://placehold.co/400x400/40E0D0/ffffff?text=Loading", 
                imagePrompt: "Aggressive gaming smartphone design with visible LED lights or transparent panel, focused on performance and speed, product photo.",
                specs: {
                    Display: ["6.78-inch AMOLED", "144Hz Ultra Refresh Rate"],
                    Camera: ["Main: 108MP (OIS)", "Dual auxiliary lenses"],
                    Platform: ["MediaTek Dimensity 8200 Ultimate", "12GB RAM LPDDR5X"],
                    Battery: ["5000mAh Capacity", "45W Fast Charging", "Dedicated X-Boost Gaming Mode"]
                }
            },
            { 
                id: 23, 
                name: "Infinix Note 40 Pro", 
                price: 36990, 
                brand: "Infinix",
                desc: "Premium mid-range phone featuring All-Round FastCharge 2.0 and a curved AMOLED display. Excellent value.", 
                image: "https://placehold.co/400x400/008080/ffffff?text=Loading", 
                imagePrompt: "Sleek mid-range Infinix phone, bright green or gold color, curved display, high-quality product shot.",
                specs: {
                    Display: ["6.78-inch Curved AMOLED", "120Hz Refresh Rate"],
                    Camera: ["Main: 108MP (OIS)", "Front: 32MP"],
                    Platform: ["MediaTek Dimensity 7020", "8GB RAM"],
                    Battery: ["5000mAh Capacity", "70W FastCharge", "20W Wireless MagCharge"]
                }
            },
            { 
                id: 24, 
                name: "Infinix Smart 8 HD", 
                price: 9999, 
                brand: "Infinix",
                desc: "Extremely affordable entry point, offering a smooth 90Hz display and a durable battery for essential connectivity.", 
                image: "https://placehold.co/400x400/FFA07A/000000?text=Loading", 
                imagePrompt: "Lowest budget Infinix phone, simple design, light blue or black color, focusing on price point, clean shot.",
                specs: {
                    Display: ["6.6-inch HD+ IPS LCD", "90Hz Refresh Rate"],
                    Camera: ["Main: 13MP Dual AI Camera"],
                    Platform: ["Unisoc T606", "3GB RAM"],
                    Battery: ["5000mAh Capacity", "10W Charging"]
                }
            },
        ];

        const apiKey = ""; // API key is handled by the environment
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/imagen-3.0-generate-002:predict?key=${apiKey}`;
        const productGrid = document.getElementById('product-grid');
        const noResultsMessage = document.getElementById('no-results');


        /**
         * Helper function to delay execution (for exponential backoff).
         * @param {number} ms - Milliseconds to wait.
         */
        function delay(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        }

        /**
         * Fetches an image from the API with exponential backoff.
         * @param {string} prompt - The image generation prompt.
         * @param {number} retries - Number of retries remaining.
         * @returns {Promise<string|null>} Base64 image data string or null on failure.
         */
        async function generateImageWithBackoff(prompt, retries = 3) {
            const payload = { 
                instances: [{ prompt: prompt }], 
                parameters: { "sampleCount": 1, "aspectRatio": "1:1" } 
            };
            
            for (let i = 0; i < retries; i++) {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        if (response.status === 429 && i < retries - 1) { // Rate limit
                            await delay(Math.pow(2, i) * 1000); // Exponential backoff
                            continue;
                        }
                        throw new Error(`API call failed with status: ${response.status}`);
                    }
                    
                    const result = await response.json();
                    
                    if (result.predictions && result.predictions.length > 0 && result.predictions[0].bytesBase64Encoded) {
                        return result.predictions[0].bytesBase64Encoded;
                    }
                    return null;
                } catch (error) {
                    if (i < retries - 1) {
                        await delay(Math.pow(2, i) * 1000); // Exponential backoff
                    } else {
                        console.error("Failed to generate image after multiple retries:", error);
                        return null;
                    }
                }
            }
            return null;
        }

        /**
         * Renders the product grid cards based on the provided list of products.
         * @param {Array} filteredProducts - The list of products to display.
         */
        function renderProducts(filteredProducts = products) {
            
            if (!productGrid) return;
            
            if (filteredProducts.length === 0) {
                productGrid.innerHTML = '';
                noResultsMessage.classList.remove('hidden');
                return;
            }

            noResultsMessage.classList.add('hidden');
            
            // Generate initial card HTML with either generated image or loading state
            productGrid.innerHTML = filteredProducts.map(product => `
                <div id="product-${product.id}" class="product-card bg-white rounded-xl shadow-lg p-6 cursor-pointer flex flex-col items-center text-center" onclick="openModal(${product.id})">
                    <!-- Image Area -->
                    <div id="image-container-${product.id}" class="h-48 w-full flex items-center justify-center mb-4 overflow-hidden rounded-lg bg-gray-200">
                        ${product.image && product.image.startsWith('data:image') ? 
                            `<img src="${product.image}" alt="${product.name}" class="object-cover w-full h-full transform transition-transform duration-300 hover:scale-105" />` :
                            `<div class="spinner text-indigo-600"></div>`
                        }
                    </div>
                    
                    <!-- Info -->
                    <span class="text-xs font-medium text-gray-500 bg-gray-100 rounded-full px-2 py-0.5 mb-2">${product.brand}</span>
                    <h3 class="text-xl font-semibold text-gray-900 mb-1">${product.name}</h3>
                    <p class="text-gray-500 text-sm mb-3">${product.desc.substring(0, 50)}...</p>
                    <p class="text-2xl font-extrabold text-purple-600 mb-4">৳${product.price.toLocaleString('en-IN')}</p>
                    
                    <!-- Button - View Specs -->
                    <button class="w-full bg-purple-100 text-purple-600 font-medium py-2 rounded-lg hover:bg-purple-600 hover:text-white transition duration-200 flex items-center justify-center space-x-2">
                        <i data-lucide="info" class="w-4 h-4"></i>
                        <span>View Specs</span>
                    </button>
                </div>
            `).join('');

            // Re-initialize Lucide icons for the newly injected content
            lucide.createIcons();
            
            // Start image generation for products that don't have a generated image yet
            generateAndSetImages(filteredProducts);
        }

        /**
         * Generates and updates images for all products that need it.
         * @param {Array} currentProducts - The list of products currently being rendered.
         */
        async function generateAndSetImages(currentProducts) {
            for (const product of currentProducts) {
                // Only generate if the image is the initial placeholder URL (not base64 data)
                if (product.image && !product.image.startsWith('data:image')) {
                    const base64Data = await generateImageWithBackoff(product.imagePrompt);
                    const container = document.getElementById(`image-container-${product.id}`);
                    
                    if (base64Data && container) {
                        const imageUrl = `data:image/png;base64,${base64Data}`;
                        
                        // Update the product object with the new image URL
                        product.image = imageUrl;

                        // Update the DOM to show the image instead of the loader
                        container.innerHTML = `
                            <img id="image-${product.id}" 
                                 src="${imageUrl}" 
                                 alt="${product.name}" 
                                 class="object-cover w-full h-full transform transition-transform duration-300 hover:scale-105" />
                        `;
                    } else if (container) {
                        // Show generic placeholder if generation fails
                         container.innerHTML = `
                            <img id="image-${product.id}" 
                                 src="https://placehold.co/400x400/94A3B8/000000?text=Image+Failed" 
                                 alt="${product.name}" 
                                 class="object-cover w-full h-full" />
                        `;
                    }
                }
            }
        }

        /**
         * Renders the dynamic brand filter dropdown options.
         */
        function renderBrandFilters() {
            const brandFilterElement = document.getElementById('brand-filter');
            if (!brandFilterElement) return;

            // 1. Get unique sorted brands
            const uniqueBrands = [...new Set(products.map(p => p.brand))].sort();

            // 2. Build options HTML
            let optionsHtml = '<option value="all">All Brands</option>';
            uniqueBrands.forEach(brand => {
                optionsHtml += `<option value="${brand}">${brand}</option>`;
            });

            // 3. Inject into the DOM
            brandFilterElement.innerHTML = optionsHtml;
        }

        /**
         * Filters the products based on the current price range AND selected brand.
         */
        function filterProducts() {
            const minInput = document.getElementById('min-price');
            const maxInput = document.getElementById('max-price');
            const brandSelect = document.getElementById('brand-filter');
            const message = document.getElementById('filter-message');

            const minPrice = parseInt(minInput.value) || 0;
            const maxPrice = parseInt(maxInput.value) || Infinity;
            const selectedBrand = brandSelect.value;
            
            // Validation
            if (minPrice > maxPrice && maxInput.value !== '') {
                message.classList.remove('hidden');
                productGrid.innerHTML = '';
                noResultsMessage.classList.add('hidden');
                return;
            } else {
                message.classList.add('hidden');
            }

            // Combined Filtering Logic
            const filtered = products.filter(product => {
                const priceMatch = product.price >= minPrice && product.price <= maxPrice;
                const brandMatch = selectedBrand === 'all' || product.brand === selectedBrand;
                return priceMatch && brandMatch;
            });

            renderProducts(filtered);
        }

        /**
         * Sets the price inputs and triggers the filter.
         * @param {number} min - Minimum price for the quick filter.
         * @param {number} max - Maximum price for the quick filter.
         */
        function setQuickFilter(min, max) {
            document.getElementById('min-price').value = min;
            document.getElementById('max-price').value = max;
            filterProducts();
        }

        /**
         * Clears all filters and resets the display.
         */
        function clearFilter() {
            document.getElementById('min-price').value = '';
            document.getElementById('max-price').value = '';
            document.getElementById('brand-filter').value = 'all'; // Reset brand filter
            document.getElementById('filter-message').classList.add('hidden');
            renderProducts(products); // Show all products
        }

        /**
         * Opens the product detail modal and injects the detailed, categorized specs.
         * (Kept the original openModal function for functionality)
         * @param {number} productId - The ID of the product to display.
         */
        function openModal(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            // Get elements
            const modal = document.getElementById('product-modal');
            const modalContentCard = document.getElementById('modal-content-card');
            
            // Populate basic modal content
            document.getElementById('modal-name').textContent = product.name;
            document.getElementById('modal-price').textContent = product.price.toLocaleString('en-IN');
            document.getElementById('modal-description').textContent = product.desc;
            
            // Use the dynamically generated image URL (or the fallback placeholder)
            document.getElementById('modal-image').src = product.image;
            document.getElementById('modal-image').alt = product.name;
            
            // Populate detailed specifications list
            const specsList = document.getElementById('modal-specs-list');
            specsList.innerHTML = ''; // Clear previous content

            for (const category in product.specs) {
                if (product.specs.hasOwnProperty(category)) {
                    // Add Category Header
                    specsList.innerHTML += `<li class="font-bold text-gray-900 mt-4 mb-1 border-b border-purple-100 pb-1">${category}</li>`;
                    
                    // Add Sub-features
                    product.specs[category].forEach(spec => {
                        specsList.innerHTML += `
                            <li class="flex items-start text-sm ml-2 py-0.5">
                                <i data-lucide="chevrons-right" class="w-4 h-4 text-purple-500 mr-2 flex-shrink-0 mt-0.5"></i> 
                                <span>${spec}</span>
                            </li>
                        `;
                    });
                }
            }
            lucide.createIcons(); // Re-initialize icons for the new list items

            // Show modal
            modal.classList.remove('hidden');
            document.body.classList.add('overflow-hidden');
            
            // Animate in
            setTimeout(() => {
                modalContentCard.classList.remove('scale-95', 'opacity-0');
                modalContentCard.classList.add('scale-100', 'opacity-100');
            }, 10);
        }

        /**
         * Closes the product detail modal.
         * @param {Event} event - Optional click event to check if click was on overlay.
         */
        function closeModal(event) {
            const modal = document.getElementById('product-modal');
            const modalContentCard = document.getElementById('modal-content-card');

            // Only close if clicked on the modal overlay itself, or if 'event' is not provided (e.g., from X button)
            if (!event || event.target === modal) {
                // Animate out
                modalContentCard.classList.remove('scale-100', 'opacity-100');
                modalContentCard.classList.add('scale-95', 'opacity-0');

                // Hide modal after transition
                setTimeout(() => {
                    modal.classList.add('hidden');
                    document.body.classList.remove('overflow-hidden');
                }, 300);
            }
        }

        // Initialize the app when the window loads
        window.onload = function() {
            renderBrandFilters(); // Initialize the brand filter dropdown
            renderProducts();
        };

        // Initialize Lucide icons after dynamic content is added
        document.addEventListener('DOMContentLoaded', () => {
             lucide.createIcons();
        });
    </script>

</body>
</html>

