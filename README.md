<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NUDE & NOIR — Luxury Minimalist Apparel</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;500;600;700&family=Inter:wght@200;300;400;500;600&display=swap" rel="stylesheet">
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        noir: {
                            900: '#0a0a0a',
                            800: '#141414',
                            700: '#1e1e1e',
                            600: '#2a2a2a',
                            muted: '#737373'
                        },
                        bone: {
                            100: '#f9f8f6',
                            200: '#f0eee8',
                            300: '#e2dec',
                            muted: '#a39e93'
                        },
                        nude: {
                            light: '#e5d4c0',
                            DEFAULT: '#d3beaf',
                            dark: '#b8a090',
                            deep: '#8c7667'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Cinzel', 'serif']
                    }
                }
            }
        }
    </script>
    
    <style>
        ::selection {
            background-color: #d3beaf;
            color: #0a0a0a;
        }
        /* Sleek custom scrollbars */
        ::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0a0a;
        }
        ::-webkit-scrollbar-thumb {
            background: #2a2a2a;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #d3beaf;
        }

        .img-zoom {
            overflow: hidden;
        }
        .img-zoom img {
            transition: transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .img-zoom:hover img {
            transform: scale(1.05);
        }

        .glass-dark {
            background: rgba(15, 15, 15, 0.88);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
        }

        .hero-overlay {
            background: linear-gradient(180deg, rgba(10,10,10,0.3) 0%, rgba(10,10,10,0.85) 80%, rgba(10,10,10,1) 100%);
        }
    </style>
</head>
<body class="bg-noir-900 text-bone-100 font-sans antialiased selection:bg-nude selection:text-noir-900 min-h-screen flex flex-col justify-between">

    <!-- Toast Notification Container -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-24 opacity-0 transition-all duration-500 pointer-events-none bg-noir-800 border border-nude/40 text-bone-100 px-6 py-4 rounded-none shadow-2xl flex items-center space-x-4 max-w-md">
        <div class="p-2 bg-nude/10 text-nude rounded-full">
            <i data-lucide="check" class="w-4 h-4"></i>
        </div>
        <div>
            <h5 id="toast-title" class="text-xs uppercase tracking-[0.2em] font-medium text-nude">Notification</h5>
            <p id="toast-message" class="text-xs text-bone-muted font-light mt-0.5 tracking-wider">Item updated.</p>
        </div>
    </div>

    <!-- Top Announcement Bar -->
    <div class="bg-noir-800 border-b border-noir-600/50 py-2 text-[10px] uppercase tracking-[0.3em] text-center font-light text-nude">
        <span>Complimentary Express Shipping on Orders Over $250 &bull; OEKO-TEX® Certified Materials</span>
    </div>

    <!-- Navigation Header -->
    <header class="sticky top-0 z-40 bg-noir-900/90 backdrop-blur-md border-b border-noir-600/40 transition-all">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Mobile Menu Toggle -->
            <button id="mobile-menu-btn" class="md:hidden text-bone-100 hover:text-nude transition p-2">
                <i data-lucide="menu" class="w-6 h-6"></i>
            </button>

            <!-- Brand Logo -->
            <a href="#" class="flex flex-col items-center group">
                <span class="font-serif text-2xl sm:text-3xl tracking-[0.25em] font-normal text-bone-100 group-hover:text-nude transition duration-300">NUDE & NOIR</span>
                <span class="text-[8px] tracking-[0.4em] text-bone-muted uppercase font-light -mt-1">High-Fashion Minimal</span>
            </a>

            <!-- Desktop Links -->
            <nav class="hidden md:flex items-center space-x-8 text-xs tracking-[0.2em] font-light uppercase">
                <a href="#catalog" onclick="filterCategory('All')" class="hover:text-nude transition-colors py-1">Catalog</a>
                <a href="#catalog" onclick="filterCategory('Tops')" class="hover:text-nude transition-colors py-1">Tops</a>
                <a href="#catalog" onclick="filterCategory('Jumpsuits & Rompers')" class="hover:text-nude transition-colors py-1">Jumpsuits</a>
                <a href="#catalog" onclick="filterCategory('Bottoms & Skirts')" class="hover:text-nude transition-colors py-1">Bottoms & Skirts</a>
                <a href="#standards" class="hover:text-nude transition-colors py-1">Safety & Fabrics</a>
            </nav>

            <!-- Header Actions -->
            <div class="flex items-center space-x-5">
                <button onclick="showToast('Wishlist feature active for saved items')" class="hidden sm:block text-bone-100 hover:text-nude transition p-1">
                    <i data-lucide="heart" class="w-5 h-5"></i>
                </button>
                
                <button id="cart-trigger" class="relative p-2 flex items-center space-x-2 text-xs tracking-widest uppercase group">
                    <span class="hidden sm:inline font-light text-bone-muted group-hover:text-bone-100 transition">Bag</span>
                    <div class="relative">
                        <i data-lucide="shopping-bag" class="w-5 h-5 group-hover:text-nude transition"></i>
                        <span id="cart-badge" class="absolute -top-1.5 -right-2 bg-nude text-noir-900 text-[10px] font-bold rounded-full w-4 h-4 flex items-center justify-center opacity-0 transition-opacity">0</span>
                    </div>
                </button>
            </div>
        </div>

        <!-- Mobile Navigation Menu Dropdown -->
        <div id="mobile-menu" class="hidden md:hidden bg-noir-800 border-b border-noir-600 px-6 py-5 flex flex-col space-y-4 text-xs tracking-[0.2em] uppercase">
            <a href="#catalog" onclick="filterCategory('All'); closeMobileMenu()" class="hover:text-nude transition py-1">Catalog</a>
            <a href="#catalog" onclick="filterCategory('Tops'); closeMobileMenu()" class="hover:text-nude transition py-1">Tops</a>
            <a href="#catalog" onclick="filterCategory('Jumpsuits & Rompers'); closeMobileMenu()" class="hover:text-nude transition py-1">Jumpsuits & Rompers</a>
            <a href="#catalog" onclick="filterCategory('Bottoms & Skirts'); closeMobileMenu()" class="hover:text-nude transition py-1">Bottoms & Skirts</a>
            <a href="#standards" onclick="closeMobileMenu()" class="hover:text-nude transition py-1">Fabric & Safety Standards</a>
        </div>
    </header>

    <main class="flex-grow">
        <!-- Hero Editorial Banner -->
        <section class="relative h-[82vh] min-h-[580px] flex items-center justify-center overflow-hidden border-b border-noir-600">
            <!-- Background Image with Overlay -->
            <div class="absolute inset-0 z-0">
                <img src="https://images.unsplash.com/photo-1490481651871-ab68de25d43d?q=80&w=2000&auto=format&fit=crop" 
                     alt="Nude and Noir Editorial Model" 
                     class="w-full h-full object-cover object-center opacity-45 scale-105 filter contrast-110" />
                <div class="absolute inset-0 hero-overlay"></div>
            </div>

            <!-- Hero Content -->
            <div class="relative z-10 text-center max-w-4xl px-4 sm:px-6 flex flex-col items-center">
                <span class="text-[11px] uppercase tracking-[0.45em] text-nude mb-4 font-light">Pre-Production Catalog &bull; Collection 01</span>
                <h1 class="font-serif text-4xl sm:text-6xl md:text-7xl lg:text-8xl tracking-wider uppercase font-normal leading-none mb-6 text-bone-100">
                    Chic. Minimal.<br><span class="italic font-light text-nude">Dramatic.</span>
                </h1>
                <p class="text-xs sm:text-sm font-light text-bone-muted max-w-xl tracking-[0.2em] leading-relaxed mb-10 uppercase">
                    Sculpted silhouettes, hypoallergenic stretch matrices, and monochromatic understated power.
                </p>
                <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-6">
                    <a href="#catalog" class="px-8 py-4 bg-nude text-noir-900 hover:bg-bone-100 transition-colors duration-300 text-xs uppercase tracking-[0.25em] font-medium">
                        Explore Collection
                    </a>
                    <a href="#standards" class="px-8 py-4 border border-bone-100/30 hover:border-nude text-bone-100 hover:text-nude transition-colors duration-300 text-xs uppercase tracking-[0.25em] font-light">
                        Safety Standards
                    </a>
                </div>
            </div>
        </section>

        <!-- Product Catalog Section -->
        <section id="catalog" class="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            
            <!-- Section Header & Controls -->
            <div class="flex flex-col md:flex-row md:items-end justify-between mb-10 pb-6 border-b border-noir-600/70 space-y-6 md:space-y-0">
                <div>
                    <span class="text-[10px] uppercase tracking-[0.35em] text-nude font-light">Fine Apparel</span>
                    <h2 class="font-serif text-3xl sm:text-4xl uppercase tracking-wider mt-1 text-bone-100">The Catalog</h2>
                </div>

                <!-- Category Filters & Sort Controls -->
                <div class="flex flex-col sm:flex-row gap-4 items-start sm:items-center">
                    <div class="flex flex-wrap gap-2 text-xs tracking-[0.2em] uppercase">
                        <button class="cat-btn active border border-nude px-4 py-2 text-nude" onclick="filterCategory('All')">All</button>
                        <button class="cat-btn border border-noir-600 px-4 py-2 text-bone-muted hover:border-nude hover:text-bone-100 transition" onclick="filterCategory('Tops')">Tops</button>
                        <button class="cat-btn border border-noir-600 px-4 py-2 text-bone-muted hover:border-nude hover:text-bone-100 transition" onclick="filterCategory('Jumpsuits & Rompers')">Jumpsuits</button>
                        <button class="cat-btn border border-noir-600 px-4 py-2 text-bone-muted hover:border-nude hover:text-bone-100 transition" onclick="filterCategory('Bottoms & Skirts')">Bottoms & Skirts</button>
                    </div>
                    <select id="sort-select" onchange="sortProducts()" class="bg-noir-800 border border-noir-600 text-bone-muted text-xs uppercase tracking-wider px-3 py-2 focus:outline-none focus:border-nude">
                        <option value="default">Sort by: Featured</option>
                        <option value="price-low">Price: Low to High</option>
                        <option value="price-high">Price: High to Low</option>
                    </select>
                </div>
            </div>

            <!-- Dynamic Product Grid -->
            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Products injected by JS -->
            </div>
        </section>

        <!-- Material Safety & Manufacturing Philosophy Section -->
        <section id="standards" class="py-24 border-t border-noir-600 bg-noir-800/60 relative overflow-hidden">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
                    <div>
                        <span class="text-[10px] uppercase tracking-[0.35em] text-nude font-light">Material Integrity</span>
                        <h2 class="font-serif text-3xl sm:text-5xl uppercase tracking-wider mt-2 mb-6 leading-tight text-bone-100">
                            Safe for Skin.<br><span class="italic text-nude font-light">Designed for Permanence.</span>
                        </h2>
                        <div class="space-y-4 text-xs text-bone-muted font-light leading-relaxed tracking-wider">
                            <p>
                                At Nude & Noir, aesthetics never compromise body safety. Every piece across our drops utilizes high-recovery Cotton-Spandex, Poly-Spandex athletic matrices, and Modal rayon blends designed to contour effortlessly without chemical irritation.
                            </p>
                            <p>
                                We enforce strict vendor compliance requiring certified non-toxic processing across all fabric mills.
                            </p>
                        </div>

                        <!-- Standards Cards Grid -->
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 mt-10 pt-8 border-t border-noir-600">
                            <div class="border border-noir-600 p-5 bg-noir-900/40">
                                <div class="flex items-center space-x-3 mb-2">
                                    <i data-lucide="shield-check" class="w-5 h-5 text-nude"></i>
                                    <h4 class="text-xs uppercase tracking-widest text-bone-100 font-medium">OEKO-TEX® Standard 100</h4>
                                </div>
                                <p class="text-[11px] text-bone-muted font-light leading-relaxed">Guaranteed free from 100+ harmful chemicals, heavy metals, and allergic triggers.</p>
                            </div>

                            <div class="border border-noir-600 p-5 bg-noir-900/40">
                                <div class="flex items-center space-x-3 mb-2">
                                    <i data-lucide="sparkles" class="w-5 h-5 text-nude"></i>
                                    <h4 class="text-xs uppercase tracking-widest text-bone-100 font-medium">Azo-Free Dyeing</h4>
                                </div>
                                <p class="text-[11px] text-bone-muted font-light leading-relaxed">Formulated with reactive non-carcinogenic dyes that retain depth wash after wash.</p>
                            </div>
                        </div>
                    </div>

                    <div class="relative">
                        <div class="aspect-[4/5] img-zoom border border-noir-600">
                            <img src="https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?q=80&w=1000&auto=format&fit=crop" 
                                 alt="Nude & Noir Craftsmanship" 
                                 class="w-full h-full object-cover grayscale contrast-125 opacity-80" />
                        </div>
                        <div class="absolute -bottom-6 -left-6 bg-noir-800 p-6 border border-noir-600 hidden sm:block max-w-xs shadow-2xl">
                            <span class="text-[10px] uppercase tracking-widest text-nude block mb-1">Architectural Fit</span>
                            <p class="text-[11px] text-bone-muted font-light">3D molded contour seams crafted to retain shape memory through repetitive wear.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="bg-noir-900 border-t border-noir-600 py-16 text-xs text-bone-muted font-light">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-10 mb-12">
                <!-- Col 1: Brand Info -->
                <div class="space-y-4">
                    <span class="font-serif text-xl tracking-[0.25em] font-normal text-bone-100 block">NUDE & NOIR</span>
                    <p class="text-bone-muted leading-relaxed max-w-xs text-[11px]">Chic, minimalist, and dramatic fashion catalog built for modern form.</p>
                </div>

                <!-- Col 2: Navigation -->
                <div>
                    <h4 class="text-bone-100 uppercase tracking-[0.2em] font-medium mb-4 text-[11px]">Collections</h4>
                    <ul class="space-y-2 uppercase tracking-widest text-[11px]">
                        <li><a href="#catalog" onclick="filterCategory('Tops')" class="hover:text-nude transition">Tops & Camis</a></li>
                        <li><a href="#catalog" onclick="filterCategory('Jumpsuits & Rompers')" class="hover:text-nude transition">Jumpsuits & Rompers</a></li>
                        <li><a href="#catalog" onclick="filterCategory('Bottoms & Skirts')" class="hover:text-nude transition">Bottoms & Skirts</a></li>
                        <li><a href="#standards" class="hover:text-nude transition">Safety Certifications</a></li>
                    </ul>
                </div>

                <!-- Col 3: Assistance -->
                <div>
                    <h4 class="text-bone-100 uppercase tracking-[0.2em] font-medium mb-4 text-[11px]">Client Care</h4>
                    <ul class="space-y-2 uppercase tracking-widest text-[11px]">
                        <li><a href="#" onclick="showToast('Support: care@nudeandnoir.com')" class="hover:text-nude transition">Sizing Advisory</a></li>
                        <li><a href="#" onclick="showToast('Complimentary shipping on orders over $250')" class="hover:text-nude transition">Shipping Policy</a></li>
                        <li><a href="#" onclick="showToast('30-day hassle free returns enabled')" class="hover:text-nude transition">Returns & Exchanges</a></li>
                    </ul>
                </div>

                <!-- Col 4: Newsletter -->
                <div>
                    <h4 class="text-bone-100 uppercase tracking-[0.2em] font-medium mb-4 text-[11px]">Private Drops</h4>
                    <p class="mb-4 text-[11px]">Subscribe for pre-order invitations and production updates.</p>
                    <form onsubmit="handleNewsletter(event)" class="flex">
                        <input type="email" placeholder="ENTER EMAIL ADDRESS" required class="bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-bone-100 text-[11px] tracking-wider focus:outline-none focus:border-nude w-full placeholder:text-noir-muted" />
                        <button type="submit" class="bg-nude text-noir-900 px-4 py-2.5 uppercase tracking-widest hover:bg-bone-100 transition">
                            <i data-lucide="arrow-right" class="w-4 h-4"></i>
                        </button>
                    </form>
                </div>
            </div>

            <div class="pt-8 border-t border-noir-600/60 flex flex-col sm:flex-row justify-between items-center space-y-4 sm:space-y-0 text-[10px] tracking-widest">
                <p>&copy; 2026 NUDE & NOIR APPAREL LTD. ALL RIGHTS RESERVED.</p>
                <div class="flex space-x-6">
                    <a href="#" class="hover:text-bone-100 transition">PRIVACY POLICY</a>
                    <a href="#" class="hover:text-bone-100 transition">TERMS OF SERVICE</a>
                </div>
            </div>
        </div>
    </footer>

    <!-- PRODUCT QUICK VIEW MODAL -->
    <div id="product-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div id="modal-backdrop" class="absolute inset-0 bg-noir-900/80 backdrop-blur-md"></div>

        <div class="relative glass-dark border border-noir-600 w-full max-w-4xl overflow-hidden shadow-2xl z-10 grid grid-cols-1 md:grid-cols-2 max-h-[90vh] overflow-y-auto">
            <button id="modal-close" class="absolute top-4 right-4 z-20 text-bone-muted hover:text-bone-100 transition p-2">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>

            <!-- Product Image -->
            <div class="h-80 md:h-full bg-noir-900 relative">
                <img id="modal-img" src="" alt="Detail View" class="w-full h-full object-cover">
            </div>

            <!-- Details -->
            <div class="p-6 md:p-8 flex flex-col justify-between">
                <div>
                    <span id="modal-category" class="text-[10px] uppercase tracking-[0.3em] text-nude font-light">Category</span>
                    <h3 id="modal-title" class="font-serif text-2xl md:text-3xl uppercase tracking-wider mt-1 mb-2 text-bone-100">Style Name</h3>
                    <p id="modal-price" class="text-base font-light text-bone-100 mb-4">$00.00</p>
                    
                    <p id="modal-desc" class="text-xs text-bone-muted font-light leading-relaxed mb-6">
                        Description text...
                    </p>

                    <!-- Safety Certificate Tag -->
                    <div class="mb-6 p-3 bg-noir-800/80 border border-noir-600 flex items-center space-x-3">
                        <i data-lucide="shield-check" class="w-4 h-4 text-nude flex-shrink-0"></i>
                        <span class="text-[10px] text-bone-muted uppercase tracking-wider font-light">OEKO-TEX® Standard 100 &bull; Azo-Free Dye Certified</span>
                    </div>

                    <!-- Colorway Selection -->
                    <div class="mb-6">
                        <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-2 font-medium">Colorway: <span id="modal-color-label" class="text-bone-100"></span></label>
                        <div id="modal-colorways" class="flex flex-wrap gap-2">
                            <!-- Injected dynamically -->
                        </div>
                    </div>

                    <!-- Size Selection -->
                    <div class="mb-6">
                        <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-2 font-medium">Select Size</label>
                        <div id="modal-sizes" class="flex gap-2">
                            <button class="size-btn border border-noir-600 px-3.5 py-2 text-xs uppercase hover:border-nude transition">XS</button>
                            <button class="size-btn border border-nude bg-nude text-noir-900 px-3.5 py-2 text-xs uppercase font-medium">S</button>
                            <button class="size-btn border border-noir-600 px-3.5 py-2 text-xs uppercase hover:border-nude transition">M</button>
                            <button class="size-btn border border-noir-600 px-3.5 py-2 text-xs uppercase hover:border-nude transition">L</button>
                            <button class="size-btn border border-noir-600 px-3.5 py-2 text-xs uppercase hover:border-nude transition">XL</button>
                        </div>
                    </div>
                </div>

                <button id="modal-add-btn" class="w-full py-4 bg-nude text-noir-900 uppercase text-xs tracking-[0.25em] font-medium hover:bg-bone-100 transition-colors">
                    Add To Bag
                </button>
            </div>
        </div>
    </div>

    <!-- SHOPPING CART DRAWER -->
    <div id="cart-drawer" class="fixed inset-0 z-50 pointer-events-none opacity-0 transition-opacity duration-300">
        <div id="cart-overlay" class="absolute inset-0 bg-noir-900/80 backdrop-blur-xs"></div>

        <div class="fixed inset-y-0 right-0 max-w-full flex pl-10">
            <div id="cart-panel" class="w-screen max-w-md bg-noir-800 border-l border-noir-600 shadow-2xl flex flex-col justify-between transform translate-x-full transition-transform duration-300 ease-in-out pointer-events-auto">
                
                <!-- Drawer Header -->
                <div class="p-6 border-b border-noir-600 flex items-center justify-between">
                    <div class="flex items-center space-x-3">
                        <i data-lucide="shopping-bag" class="w-5 h-5 text-nude"></i>
                        <h3 class="font-serif text-lg uppercase tracking-wider">Your Shopping Bag</h3>
                    </div>
                    <button id="cart-close" class="text-bone-muted hover:text-bone-100 transition">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                </div>

                <!-- Free Shipping Progress Bar -->
                <div class="px-6 py-3 bg-noir-900 border-b border-noir-600">
                    <div class="flex justify-between text-[10px] uppercase tracking-widest text-bone-muted mb-1.5">
                        <span id="shipping-progress-text">Free Express Shipping Progress</span>
                        <span id="shipping-amount-needed">$250.00 left</span>
                    </div>
                    <div class="w-full bg-noir-600 h-1 rounded-full overflow-hidden">
                        <div id="shipping-bar" class="bg-nude h-full w-0 transition-all duration-500"></div>
                    </div>
                </div>

                <!-- Drawer Items List -->
                <div id="cart-items" class="p-6 flex-grow overflow-y-auto space-y-6">
                    <!-- Dynamic -->
                </div>

                <!-- Drawer Footer & Checkout -->
                <div class="p-6 border-t border-noir-600 bg-noir-900">
                    <div class="flex justify-between items-center mb-4 text-xs tracking-widest uppercase font-light">
                        <span class="text-bone-muted">Subtotal</span>
                        <span id="cart-subtotal" class="text-bone-100 font-normal text-sm">$0.00</span>
                    </div>
                    <p class="text-[10px] text-bone-muted mb-6 font-light leading-relaxed">Taxes & express shipping calculated at checkout. Certified OEKO-TEX standard packaging.</p>
                    <button id="checkout-trigger-btn" class="w-full py-4 bg-nude text-noir-900 uppercase text-xs tracking-[0.25em] font-medium hover:bg-bone-100 transition-colors">
                        Proceed to Checkout
                    </button>
                </div>

            </div>
        </div>
    </div>

    <!-- CHECKOUT SIMULATION MODAL -->
    <div id="checkout-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div id="checkout-backdrop" class="absolute inset-0 bg-noir-900/90 backdrop-blur-md"></div>

        <div class="relative glass-dark border border-noir-600 w-full max-w-lg p-6 sm:p-8 shadow-2xl z-10 max-h-[90vh] overflow-y-auto">
            <button id="checkout-close" class="absolute top-4 right-4 text-bone-muted hover:text-bone-100 transition">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>

            <div id="checkout-form-container">
                <span class="text-[10px] uppercase tracking-[0.3em] text-nude font-light">Checkout Simulation</span>
                <h3 class="font-serif text-2xl uppercase tracking-wider mt-1 mb-6 text-bone-100">Order Confirmation</h3>

                <form onsubmit="processOrder(event)" class="space-y-4">
                    <div>
                        <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-1">Full Name</label>
                        <input type="text" required placeholder="Jane Doe" class="w-full bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-xs text-bone-100 focus:outline-none focus:border-nude" />
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-1">Email Address</label>
                        <input type="email" required placeholder="jane@example.com" class="w-full bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-xs text-bone-100 focus:outline-none focus:border-nude" />
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-1">Shipping Address</label>
                        <input type="text" required placeholder="123 Fashion Ave, Suite 400" class="w-full bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-xs text-bone-100 focus:outline-none focus:border-nude" />
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-1">Card Number (Demo)</label>
                            <input type="text" required placeholder="•••• •••• •••• 4242" class="w-full bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-xs text-bone-100 focus:outline-none focus:border-nude" />
                        </div>
                        <div>
                            <label class="block text-[10px] uppercase tracking-widest text-bone-muted mb-1">Expiry / CVC</label>
                            <input type="text" required placeholder="12/28 • 123" class="w-full bg-noir-800 border border-noir-600 px-3.5 py-2.5 text-xs text-bone-100 focus:outline-none focus:border-nude" />
                        </div>
                    </div>

                    <div class="pt-4 border-t border-noir-600 flex justify-between items-center text-xs tracking-widest uppercase">
                        <span>Total Amount</span>
                        <span id="checkout-total-val" class="font-normal text-nude">$0.00</span>
                    </div>

                    <button type="submit" class="w-full py-4 mt-2 bg-nude text-noir-900 uppercase text-xs tracking-[0.25em] font-medium hover:bg-bone-100 transition-colors">
                        Place Demo Order
                    </button>
                </form>
            </div>

            <!-- Confirmation View -->
            <div id="checkout-success-container" class="hidden text-center py-8">
                <div class="w-12 h-12 bg-nude/10 text-nude rounded-full flex items-center justify-center mx-auto mb-4">
                    <i data-lucide="check-circle" class="w-6 h-6"></i>
                </div>
                <span class="text-[10px] uppercase tracking-[0.3em] text-nude font-light">Order Confirmed</span>
                <h3 class="font-serif text-2xl uppercase tracking-wider mt-1 mb-2 text-bone-100">Thank You</h3>
                <p class="text-xs text-bone-muted font-light leading-relaxed mb-6">
                    Your production pre-order has been logged successfully. Confirmation email dispatched.
                </p>
                <button onclick="closeCheckoutSuccess()" class="px-8 py-3 bg-noir-800 border border-noir-600 text-bone-100 text-xs uppercase tracking-widest hover:border-nude">
                    Back to Catalog
                </button>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT APP LOGIC -->
    <script>
        // Catalog Data Repository
        const PRODUCTS = [
            {
                id: 'nn-01',
                name: 'The Apex V-Neck Tee',
                category: 'Tops',
                price: 75,
                image: 'https://images.unsplash.com/photo-1521572267360-ee0c2909d518?q=80&w=800&auto=format&fit=crop',
                colors: ['Chalk Bone', 'Obsidian Minimal', 'Barely Beige'],
                description: 'Deep plunging V-neck short-sleeve top engineered from ultra-soft modal stretch blend with clean raw-edge hems.'
            },
            {
                id: 'nn-02',
                name: 'The Vanguard Ribbed Top',
                category: 'Tops',
                price: 95,
                image: 'https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?q=80&w=800&auto=format&fit=crop',
                colors: ['Ivory Vanguard', 'Moss Vanguard', 'Midnight Vanguard'],
                description: 'Long-sleeve ribbed collared top with concealed quarter zip detailing. OEKO-TEX standard 100 cotton-spandex.'
            },
            {
                id: 'nn-03',
                name: 'The Drape & Tie Top',
                category: 'Tops',
                price: 115,
                image: 'https://images.unsplash.com/photo-1539109136881-3be0616acf4b?q=80&w=800&auto=format&fit=crop',
                colors: ['Wine Minimal', 'Silk Nude', 'Noir Draping'],
                description: 'Cowl-neck side-tie ruched top crafted with fluid rayon drape and asymmetry waist cut.'
            },
            {
                id: 'nn-04',
                name: 'The Botanica Flared Pant',
                category: 'Bottoms & Skirts',
                price: 145,
                image: 'https://images.unsplash.com/photo-1509631179647-0177331693ae?q=80&w=800&auto=format&fit=crop',
                colors: ['Cocoa Blossom', 'Noir Rosette', 'Sand Petal'],
                description: 'Sculpted foldover flare trousers featuring handcrafted 3D rosette and cascading side drape detailing.'
            },
            {
                id: 'nn-05',
                name: 'The Contour Bandeau Jumpsuit',
                category: 'Jumpsuits & Rompers',
                price: 185,
                image: 'https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?q=80&w=800&auto=format&fit=crop',
                colors: ['Ecru Contour', 'Desert Contour', 'Obsidian Contour'],
                description: 'Ribbed strapless bandeau jumpsuit with internal silicone grip lining and high compression stretch.'
            },
            {
                id: 'nn-06',
                name: 'The Cascade Ruffle Skirt',
                category: 'Bottoms & Skirts',
                price: 125,
                image: 'https://images.unsplash.com/photo-1583496661160-fb5886a0aaaa?q=80&w=800&auto=format&fit=crop',
                colors: ['Cocoa Cascade', 'Midnight Ruffle', 'Silk Cascade'],
                description: 'Tiered ruffle mini skirt featuring sheer side drapes over a built-in bodycon compression short.'
            },
            {
                id: 'nn-07',
                name: 'The Noir Lace Off-Shoulder Top',
                category: 'Tops',
                price: 105,
                image: 'https://images.unsplash.com/photo-1496747611176-843222e1e57c?q=80&w=800&auto=format&fit=crop',
                colors: ['Midnight Lace', 'Wine Lace', 'Bone Lace'],
                description: 'Ribbed long-sleeve off-shoulder top lined with delicate eyelash lace trim along collar and hem.'
            },
            {
                id: 'nn-08',
                name: 'The Asymmetry Long-Sleeve',
                category: 'Tops',
                price: 90,
                image: 'https://images.unsplash.com/photo-1445205170230-053b83016050?q=80&w=800&auto=format&fit=crop',
                colors: ['Slate Asymmetry', 'Noir Asymmetry', 'Ivory Asymmetry'],
                description: 'Architectural one-shoulder long-sleeve top with diagonal neckline and subtle gather along waist.'
            }
        ];

        // App State
        let cart = [];
        let activeCategory = 'All';
        let selectedProduct = null;
        let selectedColor = '';
        let selectedSize = 'S';

        // DOM Initialization
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            renderCatalog();
            setupEventListeners();
        });

        // Render Catalog Grid
        function renderCatalog() {
            const container = document.getElementById('product-grid');
            container.innerHTML = '';

            let items = activeCategory === 'All' 
                ? [...PRODUCTS] 
                : PRODUCTS.filter(p => p.category === activeCategory);

            // Apply Sort
            const sortVal = document.getElementById('sort-select').value;
            if (sortVal === 'price-low') items.sort((a, b) => a.price - b.price);
            if (sortVal === 'price-high') items.sort((a, b) => b.price - a.price);

            items.forEach(product => {
                const card = document.createElement('div');
                card.className = 'group relative flex flex-col justify-between border border-noir-600/60 bg-noir-800/20 p-4 transition-all duration-300 hover:border-nude/50';
                card.innerHTML = `
                    <div>
                        <div class="aspect-[3/4] w-full img-zoom bg-noir-800 relative mb-4 cursor-pointer" onclick="openProductModal('${product.id}')">
                            <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover">
                            <button class="absolute bottom-3 right-3 bg-noir-900/90 backdrop-blur-md p-2 rounded-full text-bone-100 hover:text-nude transition opacity-0 group-hover:opacity-100">
                                <i data-lucide="eye" class="w-4 h-4"></i>
                            </button>
                        </div>
                        <span class="text-[9px] uppercase tracking-[0.25em] text-nude font-light block mb-1">${product.category}</span>
                        <h3 class="font-serif text-base uppercase tracking-wider text-bone-100 group-hover:text-nude transition cursor-pointer" onclick="openProductModal('${product.id}')">${product.name}</h3>
                        <p class="text-[11px] text-bone-muted font-light mt-1">${product.colors[0]}</p>
                    </div>
                    <div class="mt-4 pt-4 border-t border-noir-600/40 flex items-center justify-between">
                        <span class="text-xs font-light text-bone-100">$${product.price.toFixed(2)}</span>
                        <button onclick="quickAddToCart('${product.id}')" class="text-[11px] uppercase tracking-widest text-bone-muted hover:text-nude transition flex items-center space-x-1">
                            <span>Add</span>
                            <i data-lucide="plus" class="w-3.5 h-3.5"></i>
                        </button>
                    </div>
                `;
                container.appendChild(card);
            });
            lucide.createIcons();
        }

        function filterCategory(category) {
            activeCategory = category;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                const text = btn.innerText;
                if ((category === 'All' && text === 'ALL') || 
                    (category === 'Tops' && text === 'TOPS') ||
                    (category === 'Jumpsuits & Rompers' && text === 'JUMPSUITS') ||
                    (category === 'Bottoms & Skirts' && text.includes('BOTTOMS'))) {
                    btn.className = 'cat-btn active border border-nude px-4 py-2 text-nude';
                } else {
                    btn.className = 'cat-btn border border-noir-600 px-4 py-2 text-bone-muted hover:border-nude hover:text-bone-100 transition';
                }
            });
            renderCatalog();
        }

        function sortProducts() {
            renderCatalog();
        }

        function closeMobileMenu() {
            document.getElementById('mobile-menu').classList.add('hidden');
        }

        // Quick View Modal
        function openProductModal(productId) {
            selectedProduct = PRODUCTS.find(p => p.id === productId);
            if (!selectedProduct) return;

            selectedColor = selectedProduct.colors[0];
            selectedSize = 'S';

            document.getElementById('modal-img').src = selectedProduct.image;
            document.getElementById('modal-category').innerText = selectedProduct.category;
            document.getElementById('modal-title').innerText = selectedProduct.name;
            document.getElementById('modal-price').innerText = `$${selectedProduct.price.toFixed(2)}`;
            document.getElementById('modal-desc').innerText = selectedProduct.description;
            document.getElementById('modal-color-label').innerText = selectedColor;

            // Swatches
            const colorContainer = document.getElementById('modal-colorways');
            colorContainer.innerHTML = '';
            selectedProduct.colors.forEach((color, idx) => {
                const btn = document.createElement('button');
                btn.className = `text-xs px-3 py-1.5 uppercase border transition ${idx === 0 ? 'border-nude text-nude font-medium' : 'border-noir-600 text-bone-muted hover:border-nude'}`;
                btn.innerText = color;
                btn.onclick = () => {
                    selectedColor = color;
                    document.getElementById('modal-color-label').innerText = color;
                    Array.from(colorContainer.children).forEach(c => c.className = 'text-xs px-3 py-1.5 uppercase border border-noir-600 text-bone-muted hover:border-nude');
                    btn.className = 'text-xs px-3 py-1.5 uppercase border border-nude text-nude font-medium';
                };
                colorContainer.appendChild(btn);
            });

            // Size buttons
            document.querySelectorAll('#modal-sizes .size-btn').forEach(btn => {
                btn.onclick = () => {
                    selectedSize = btn.innerText;
                    document.querySelectorAll('#modal-sizes .size-btn').forEach(b => b.className = 'size-btn border border-noir-600 px-3.5 py-2 text-xs uppercase hover:border-nude transition');
                    btn.className = 'size-btn border border-nude bg-nude text-noir-900 px-3.5 py-2 text-xs uppercase font-medium';
                };
            });

            const modal = document.getElementById('product-modal');
            modal.classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeModal() {
            const modal = document.getElementById('product-modal');
            modal.classList.add('opacity-0', 'pointer-events-none');
        }

        // Cart Actions
        function quickAddToCart(productId) {
            const prod = PRODUCTS.find(p => p.id === productId);
            if (prod) {
                addToCart(prod, prod.colors[0], 'S');
            }
        }

        function addToCart(product, color, size) {
            const existingIndex = cart.findIndex(i => i.id === product.id && i.color === color && i.size === size);
            if (existingIndex > -1) {
                cart[existingIndex].qty += 1;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    image: product.image,
                    color: color,
                    size: size,
                    qty: 1
                });
            }
            updateCartUI();
            showToast(`${product.name} (${color}) added to bag.`);
        }

        function updateCartUI() {
            const container = document.getElementById('cart-items');
            const badge = document.getElementById('cart-badge');
            const subtotalEl = document.getElementById('cart-subtotal');
            const shippingBar = document.getElementById('shipping-bar');
            const shippingNeeded = document.getElementById('shipping-amount-needed');

            const totalItems = cart.reduce((acc, i) => acc + i.qty, 0);
            const subtotal = cart.reduce((acc, i) => acc + (i.price * i.qty), 0);

            // Badge
            if (totalItems > 0) {
                badge.innerText = totalItems;
                badge.classList.remove('opacity-0');
            } else {
                badge.classList.add('opacity-0');
            }

            // Subtotal
            subtotalEl.innerText = `$${subtotal.toFixed(2)}`;

            // Free shipping bar ($250 target)
            const target = 250;
            const progress = Math.min((subtotal / target) * 100, 100);
            shippingBar.style.width = `${progress}%`;
            if (subtotal >= target) {
                shippingNeeded.innerText = 'Unlocked Free Express';
            } else {
                shippingNeeded.innerText = `$${(target - subtotal).toFixed(2)} left`;
            }

            // Render list
            if (cart.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-16 text-bone-muted">
                        <i data-lucide="shopping-bag" class="w-10 h-10 mx-auto mb-3 opacity-30 text-nude"></i>
                        <p class="text-xs uppercase tracking-widest font-light">Your shopping bag is empty.</p>
                    </div>
                `;
            } else {
                container.innerHTML = '';
                cart.forEach((item, index) => {
                    const el = document.createElement('div');
                    el.className = 'flex space-x-4 border-b border-noir-600/60 pb-4';
                    el.innerHTML = `
                        <img src="${item.image}" class="w-16 h-20 object-cover bg-noir-900 border border-noir-600">
                        <div class="flex-grow flex flex-col justify-between">
                            <div>
                                <div class="flex justify-between items-start">
                                    <h4 class="text-xs font-serif uppercase tracking-wider text-bone-100">${item.name}</h4>
                                    <button onclick="removeCartItem(${index})" class="text-bone-muted hover:text-bone-100">
                                        <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                                    </button>
                                </div>
                                <p class="text-[10px] text-nude uppercase tracking-widest mt-0.5">${item.color} &bull; Size ${item.size}</p>
                            </div>
                            <div class="flex justify-between items-center mt-2 text-xs">
                                <div class="flex items-center border border-noir-600">
                                    <button onclick="changeQty(${index}, -1)" class="px-2 py-0.5 text-bone-muted hover:text-bone-100">-</button>
                                    <span class="px-2 text-[11px] text-bone-100">${item.qty}</span>
                                    <button onclick="changeQty(${index}, 1)" class="px-2 py-0.5 text-bone-muted hover:text-bone-100">+</button>
                                </div>
                                <span class="font-light text-bone-100">$${(item.price * item.qty).toFixed(2)}</span>
                            </div>
                        </div>
                    `;
                    container.appendChild(el);
                });
            }
            lucide.createIcons();
        }

        function changeQty(index, delta) {
            cart[index].qty += delta;
            if (cart[index].qty <= 0) cart.splice(index, 1);
            updateCartUI();
        }

        function removeCartItem(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function toggleCartDrawer(open) {
            const drawer = document.getElementById('cart-drawer');
            const panel = document.getElementById('cart-panel');
            if (open) {
                drawer.classList.remove('pointer-events-none', 'opacity-0');
                panel.classList.remove('translate-x-full');
            } else {
                panel.classList.add('translate-x-full');
                setTimeout(() => drawer.classList.add('pointer-events-none', 'opacity-0'), 300);
            }
        }

        // Checkout Simulation
        function openCheckout() {
            if (cart.length === 0) {
                showToast('Bag is empty.');
                return;
            }
            toggleCartDrawer(false);
            const subtotal = cart.reduce((acc, i) => acc + (i.price * i.qty), 0);
            document.getElementById('checkout-total-val').innerText = `$${subtotal.toFixed(2)}`;
            document.getElementById('checkout-form-container').classList.remove('hidden');
            document.getElementById('checkout-success-container').classList.add('hidden');
            
            const modal = document.getElementById('checkout-modal');
            modal.classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeCheckout() {
            const modal = document.getElementById('checkout-modal');
            modal.classList.add('opacity-0', 'pointer-events-none');
        }

        function processOrder(e) {
            e.preventDefault();
            document.getElementById('checkout-form-container').classList.add('hidden');
            document.getElementById('checkout-success-container').classList.remove('hidden');
            cart = [];
            updateCartUI();
        }

        function closeCheckoutSuccess() {
            closeCheckout();
        }

        // Toast Notification System
        function showToast(message) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = message;
            toast.classList.remove('translate-y-24', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3200);
        }

        function handleNewsletter(e) {
            e.preventDefault();
            showToast('Invited to private pre-order catalog drops.');
            e.target.reset();
        }

        // Setup All Event Listeners
        function setupEventListeners() {
            document.getElementById('mobile-menu-btn').addEventListener('click', () => {
                document.getElementById('mobile-menu').classList.toggle('hidden');
            });

            document.getElementById('cart-trigger').addEventListener('click', () => toggleCartDrawer(true));
            document.getElementById('cart-close').addEventListener('click', () => toggleCartDrawer(false));
            document.getElementById('cart-overlay').addEventListener('click', () => toggleCartDrawer(false));

            document.getElementById('modal-close').addEventListener('click', closeModal);
            document.getElementById('modal-backdrop').addEventListener('click', closeModal);

            document.getElementById('modal-add-btn').addEventListener('click', () => {
                if (selectedProduct) {
                    addToCart(selectedProduct, selectedColor, selectedSize);
                    closeModal();
                    toggleCartDrawer(true);
                }
            });

            document.getElementById('checkout-trigger-btn').addEventListener('click', openCheckout);
            document.getElementById('checkout-close').addEventListener('click', closeCheckout);
            document.getElementById('checkout-backdrop').addEventListener('click', closeCheckout);
        }
    </script>
</body>
</html>
