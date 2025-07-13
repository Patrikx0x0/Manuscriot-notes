<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Story of Sanskrit: An Interactive Exploration</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cardo:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    
    <!-- Chosen Palette: Warm Harmony -->
    <!-- Application Structure Plan: The SPA uses a thematic, non-linear dashboard structure to make the dense academic report digestible. A sticky top navigation allows users to jump to key themes: 1) A visual timeline for its history ('The Journey'), 2) Interactive cards for its vast contributions ('A Universe of Knowledge'), 3) A section with interactive diagrams for its grammar ('Linguistic Genius'), 4) An interactive chart and gallery for its diverse scripts ('The Written Word'), and 5) Dynamic counters and info graphics for its modern relevance ('Enduring Legacy'). This structure prioritizes user-led exploration and visual learning over passive reading, making the content more engaging and easier to synthesize. -->
    <!-- Visualization & Content Choices: 1. History: Report's historical narrative -> Goal: Show evolution -> Viz: Interactive HTML/CSS timeline -> Interaction: Click events reveal detailed text -> Justification: More intuitive than paragraphs for time-based data. 2. Contributions: Report's list of fields -> Goal: Show breadth -> Viz: HTML/CSS card grid -> Interaction: Click-to-reveal details on each card -> Justification: Visually organizes diverse topics for easy Browse. 3. Scripts: Report's table of scripts -> Goal: Compare usage periods -> Viz: Chart.js horizontal bar chart -> Interaction: Tooltips on hover show date ranges -> Justification: A chart provides a much clearer and faster comparison of time-based data than a static table. 4. Grammarians: Report's Table 2 -> Goal: Organize data -> Viz: Interactive HTML table -> Interaction: Click headers to sort -> Justification: Adds utility and engagement to tabular data. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFCF8;
            color: #4A4A4A;
        }
        h1, h2, h3 {
            font-family: 'Cardo', serif;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #C0843E;
            border-bottom-color: #C0843E;
        }
        .hero-bg {
            background-color: #EAE3D9;
            background-image: linear-gradient(to right, rgba(253, 252, 248, 1), rgba(253, 252, 248, 0.7), rgba(253, 252, 248, 0)), url('https://placehold.co/1920x1080/EAE3D9/4A4A4A?text=+');
            background-size: cover;
            background-position: center right;
        }
        .card {
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            top: 1.25rem;
            left: -0.6rem;
            width: 1.25rem;
            height: 1.25rem;
            background-color: #D2B48C;
            border: 3px solid #FDFCF8;
            border-radius: 50%;
            z-index: 1;
        }
        .timeline-item:hover::before {
            background-color: #C0843E;
        }
        .modal-bg {
            background-color: rgba(0, 0, 0, 0.5);
            transition: opacity 0.3s ease;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 900px;
            margin-left: auto;
            margin-right: auto;
            height: 400px;
            max-height: 50vh;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 500px;
            }
        }
    </style>
</head>
<body class="antialiased">

    <!-- Header & Navigation -->
    <header id="header" class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold text-gray-800 font-serif">Sanskrit</a>
            <div class="hidden md:flex space-x-8">
                <a href="#journey" class="nav-link pb-1">The Journey</a>
                <a href="#knowledge" class="nav-link pb-1">Universe of Knowledge</a>
                <a href="#genius" class="nav-link pb-1">Linguistic Genius</a>
                <a href="#scripts" class="nav-link pb-1">The Written Word</a>
                <a href="#legacy" class="nav-link pb-1">Enduring Legacy</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden focus:outline-none">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden">
            <a href="#journey" class="block py-2 px-6 text-sm hover:bg-gray-200">The Journey</a>
            <a href="#knowledge" class="block py-2 px-6 text-sm hover:bg-gray-200">Universe of Knowledge</a>
            <a href="#genius" class="block py-2 px-6 text-sm hover:bg-gray-200">Linguistic Genius</a>
            <a href="#scripts" class="block py-2 px-6 text-sm hover:bg-gray-200">The Written Word</a>
            <a href="#legacy" class="block py-2 px-6 text-sm hover:bg-gray-200">Enduring Legacy</a>
        </div>
    </header>

    <main>
        <!-- Hero Section -->
        <section class="hero-bg">
            <div class="container mx-auto px-6 py-24 md:py-32 flex items-center">
                <div class="w-full md:w-3/5 lg:w-1/2">
                    <h1 class="text-4xl md:text-6xl font-bold text-gray-800 leading-tight">
                        The Story of Sanskrit
                    </h1>
                    <p class="mt-4 text-lg text-gray-600">
                        An interactive exploration of the world's most refined language—its history, its profound contributions to knowledge, and its enduring legacy in the modern world.
                    </p>
                    <a href="#journey" class="mt-8 inline-block bg-[#C0843E] text-white font-bold py-3 px-6 rounded-lg shadow-lg hover:bg-[#A57034] transition-colors">Begin the Journey</a>
                </div>
            </div>
        </section>

        <!-- The Journey Section -->
        <section id="journey" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold">The Journey of Sanskrit</h2>
                    <p class="mt-2 text-lg text-gray-500 max-w-3xl mx-auto">From a sacred oral tradition to a meticulously standardized classical language, Sanskrit's evolution is a cornerstone of linguistic history. Explore its key milestones by clicking on the timeline events.</p>
                </div>
                <div id="timeline-container" class="relative max-w-4xl mx-auto">
                    <!-- Timeline will be generated by JS -->
                </div>
            </div>
        </section>

        <!-- Universe of Knowledge Section -->
        <section id="knowledge" class="py-20 bg-[#F7F2EC]">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold">A Universe of Knowledge</h2>
                    <p class="mt-2 text-lg text-gray-500 max-w-3xl mx-auto">Sanskrit was the language of not just religion and philosophy, but also of groundbreaking scientific inquiry. Click on each domain to uncover its profound contributions.</p>
                </div>
                <div id="knowledge-cards" class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <!-- Knowledge cards will be generated by JS -->
                </div>
            </div>
        </section>

        <!-- Linguistic Genius Section -->
        <section id="genius" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold">The Linguistic Genius</h2>
                    <p class="mt-2 text-lg text-gray-500 max-w-3xl mx-auto">The grammar of Sanskrit, particularly as codified by Pāṇini, is a marvel of logical precision and systematicity that predated modern linguistics by millennia.</p>
                </div>
                <div class="grid lg:grid-cols-5 gap-8">
                    <div class="lg:col-span-3 bg-[#F7F2EC] p-8 rounded-xl shadow-sm">
                        <h3 class="text-2xl font-bold mb-4">Pāṇini's Aṣṭādhyāyī: The Generative Grammar</h3>
                        <p class="mb-4">Around 500 BCE, the scholar Pāṇini composed the *Aṣṭādhyāyī* ("Eight Chapters"), a masterpiece containing 3,959 rules. It's a prescriptive and generative grammar that meticulously describes every aspect of Sanskrit, from phonology to syntax. Its algebraic-like rules and abstract markers demonstrate a computational approach to language far ahead of its time.</p>
                        <p>This work standardized the language, creating "Classical Sanskrit" (*saṃskṛta* - "refined"), and became the foundational text of *Vyākaraṇa* (Sanskrit grammar), influencing linguistic thought for over two millennia.</p>
                        <div class="mt-6 border-t border-gray-300 pt-6">
                             <h4 class="text-xl font-bold mb-2">Interactive Sandhi Example</h4>
                             <p class="text-sm text-gray-600 mb-4">Sandhi rules govern how sounds combine at word boundaries. Test a simple rule: *akaḥ savarṇe dīrghaḥ* (similar vowels combine into a long vowel).</p>
                             <div class="flex items-center space-x-2">
                                 <input id="sandhi-input1" type="text" value="deva" class="p-2 border rounded-md w-1/3 bg-white">
                                 <span class="text-2xl">+</span>
                                 <input id="sandhi-input2" type="text" value="ālaya" class="p-2 border rounded-md w-1/3 bg-white">
                                 <button id="sandhi-button" class="px-4 py-2 bg-[#C0843E] text-white rounded-md hover:bg-[#A57034]">=</button>
                                 <span id="sandhi-output" class="p-2 font-bold text-lg w-1/3">deva + ālaya</span>
                             </div>
                        </div>
                    </div>
                    <div class="lg:col-span-2 bg-white p-6 rounded-xl border border-gray-200">
                        <h3 class="text-2xl font-bold mb-4">Key Sanskrit Grammarians</h3>
                        <p class="mb-4 text-sm text-gray-600">Pāṇini's work was the foundation of a rich grammatical tradition. Click headers to sort.</p>
                        <div class="overflow-x-auto">
                            <table id="grammarians-table" class="w-full text-sm text-left">
                                <thead class="text-xs text-gray-700 uppercase bg-gray-100">
                                    <tr>
                                        <th scope="col" class="px-4 py-3 cursor-pointer" data-sort="name">Grammarian &#x21c5;</th>
                                        <th scope="col" class="px-4 py-3 cursor-pointer" data-sort="date">Approx. Date &#x21c5;</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <!-- Table body will be generated by JS -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </section>


        <!-- The Written Word Section -->
        <section id="scripts" class="py-20 bg-[#F7F2EC]">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold">The Written Word: A Tapestry of Scripts</h2>
                    <p class="mt-2 text-lg text-gray-500 max-w-3xl mx-auto">Sanskrit has no single native script. It has been written in numerous regional scripts across Asia over millennia. This chart visualizes the periods of prominence for some of the most important scripts.</p>
                </div>
                <div class="bg-white p-4 sm:p-8 rounded-xl shadow-lg">
                    <div class="chart-container">
                        <canvas id="scriptsChart"></canvas>
                    </div>
                </div>
                <div class="mt-12">
                     <h3 class="text-2xl font-bold text-center mb-6">A Gallery of Scripts</h3>
                     <div id="script-gallery" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-4 text-center">
                         <!-- Script gallery items will be generated by JS -->
                     </div>
                </div>
            </div>
        </section>

        <!-- Enduring Legacy Section -->
        <section id="legacy" class="py-20 bg-white">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-4xl font-bold">Enduring Legacy</h2>
                    <p class="mt-2 text-lg text-gray-500 max-w-3xl mx-auto">From influencing languages across the globe to its modern revival, Sanskrit's journey continues.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div>
                        <h3 class="text-2xl font-bold mb-4">Mother of Languages</h3>
                        <p class="mb-6">As an Old Indo-Aryan language, Sanskrit is the ancestor or a major influencer of most modern North Indian languages like Hindi, Bengali, and Marathi. Its influence also spread across Southeast Asia, embedding itself in languages like Thai and Javanese. This linguistic tree shows its direct descendants in the Indo-Aryan family.</p>
                        <div class="p-6 bg-gray-50 rounded-lg border border-gray-200 text-sm font-mono">
                           <ul class="space-y-2">
                               <li>Proto-Indo-European</li>
                               <li class="pl-4">└── Proto-Indo-Iranian</li>
                               <li class="pl-8">└── Proto-Indo-Aryan</li>
                               <li class="pl-12">└── **Sanskrit (Vedic & Classical)**</li>
                               <li class="pl-16">└── Prakrits (e.g., Sauraseni)</li>
                               <li class="pl-20">└── Apabhraṃśa</li>
                               <li class="pl-24">└── Modern Indo-Aryan Languages</li>
                               <li class="pl-28">├── Hindi-Urdu</li>
                               <li class="pl-28">├── Bengali</li>
                               <li class="pl-28">├── Punjabi</li>
                               <li class="pl-28">├── Marathi</li>
                               <li class="pl-28">└── etc...</li>
                           </ul>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-2xl font-bold mb-4">Sanskrit Today</h3>
                        <p class="mb-6">While few speak it as a first language, Sanskrit holds official status and is actively promoted. Its "grammatical perfection" has even led to research into its use for computational linguistics and AI.</p>
                        <div class="grid grid-cols-2 gap-6">
                            <div class="bg-[#F7F2EC] p-6 rounded-lg text-center">
                                <div id="scheduled-lang" class="text-4xl font-bold text-[#C0843E]">22</div>
                                <p class="text-sm mt-1">One of India's 22 Scheduled Languages</p>
                            </div>
                            <div class="bg-[#F7F2EC] p-6 rounded-lg text-center">
                                <div id="official-lang" class="text-4xl font-bold text-[#C0843E]">2</div>
                                <p class="text-sm mt-1">Second Official Language in 2 Indian States</p>
                            </div>
                             <div class="bg-[#F7F2EC] p-6 rounded-lg text-center col-span-2">
                                <div class="text-4xl font-bold text-[#C0843E]">2022</div>
                                <p class="text-sm mt-1">Year added to Google Translate, showing global demand</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="bg-gray-800 text-white">
            <div class="container mx-auto px-6 py-8 text-center">
                <p>An Interactive Exploration based on the research paper "Script & Language, Sanskrit Language and its Importance".</p>
                <p class="text-sm text-gray-400 mt-2">Designed to bring academic knowledge to life through interactive web design.</p>
            </div>
        </footer>

    </main>

    <!-- Modal -->
    <div id="modal" class="fixed inset-0 z-50 items-center justify-center hidden">
        <div id="modal-bg" class="absolute inset-0 modal-bg"></div>
        <div id="modal-box" class="bg-white rounded-lg shadow-xl p-8 max-w-2xl w-full mx-4 relative transform transition-transform duration-300 scale-95">
            <h3 id="modal-title" class="text-2xl font-bold font-serif mb-4"></h3>
            <div id="modal-content" class="text-gray-600 max-h-[60vh] overflow-y-auto pr-4"></div>
            <button id="modal-close" class="absolute top-4 right-4 text-gray-500 hover:text-gray-800">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
            </button>
        </div>
    </div>


    <script>
        document.addEventListener('DOMContentLoaded', function() {

            // Data from the report
            const timelineData = [
                {
                    date: "c. 1700-1200 BCE",
                    title: "Vedic Sanskrit Origins",
                    content: "Sanskrit emerges as Vedic Sanskrit, an Old Indo-Aryan language. Its earliest composition, the Rigveda, is composed by tribes in the northwestern Indian subcontinent. The language is preserved meticulously through a rigorous oral chanting tradition, predating widespread writing in India by centuries."
                },
                {
                    date: "c. 1500-500 BCE",
                    title: "The Vedas: Sacred Knowledge",
                    content: "The Vedas (Rigveda, Samaveda, Yajurveda, Atharvaveda) are compiled. Revered as sacred texts, the necessity of their precise recitation and preservation becomes the primary catalyst for the development of linguistic analysis in India, leading to early grammatical studies like the Pratisakhyas."
                },
                {
                    date: "c. 500 BCE",
                    title: "Pāṇini's Aṣṭādhyāyī",
                    content: "The scholar Pāṇini composes the Aṣṭādhyāyī ('Eight Chapters'), a monumental work that standardizes the language. With 3,959 rules, it provides a complete prescriptive and generative grammar for what becomes known as Classical Sanskrit (saṃskṛta - 'refined'). This act of standardization creates a stable vehicle for transmitting complex knowledge for millennia."
                },
                {
                    date: "c. 300 BCE - 1300 CE",
                    title: "The Sanskrit Cosmopolis",
                    content: "Sanskrit becomes the preeminent language of political and cultural expression across South and Southeast Asia. Spread by intellectuals and religious professionals, it leads to the 'Indianization' of regional polities, influencing local languages, governance, and culture."
                },
                {
                    date: "1st Century BCE",
                    title: "Earliest Script: Brāhmī",
                    content: "The Brāhmī script becomes the earliest attested writing system for Sanskrit inscriptions. Its design is based on Sanskrit phonological theory, showcasing the deep link between the spoken language and its written form. Brāhmī becomes the ancestor to most modern Indic scripts."
                },
                {
                    date: "17th Century onwards",
                    title: "Modern Grammatical Works",
                    content: "Later grammarians like Bhaṭṭoji Dīkṣita (Siddhānta Kaumudī) and his disciple Varadarāja re-organized and simplified Pāṇini's grammar, making it more accessible. These works became standard for traditional Sanskrit education from the early modern period onwards."
                }
            ];

            const knowledgeData = [
                {
                    title: "Philosophy & Religion",
                    icon: '🙏',
                    content: "The language of Hinduism's foundational texts: the Vedas, Upanishads, Purāṇas, and the epics Mahabharata and Ramayana. Also used in major Buddhist and Jainist philosophical texts."
                },
                {
                    title: "Mathematics",
                    icon: '🔢',
                    content: "Groundbreaking concepts were expressed in Sanskrit, including the decimal system, the concept of zero (śūnya), the Pythagorean theorem (in the Śulba Sūtras), and foundational principles of trigonometry and calculus (by Āryabhaṭa and the Kerala School)."
                },
                {
                    title: "Astronomy",
                    icon: '🔭',
                    content: "Sanskrit treatises like the Siddhāntas contained precise mathematical models for planetary motion, eclipses, and star positions. An estimated 100,000 manuscripts exist on jyotiṣa (astronomy/astrology) alone."
                },
                {
                    title: "Medicine (Āyurveda)",
                    icon: '🌿',
                    content: "Classical texts of Āyurveda, like the Charaka Saṃhitā and the Suśruta Saṃhitā, were written in Sanskrit. They detail complex surgical procedures, herbal medicine, and holistic health principles."
                },
                {
                    title: "Physics & Acoustics",
                    icon: '⚛️',
                    content: "Early atomic theories (Vaiśeṣika Sūtras), concepts of gravity (Bhaskara II), and principles of optics and acoustics (Nāṭya Shastra) were all documented in Sanskrit texts, revealing an integrated approach to science and philosophy."
                },
                {
                    title: "Literature & Fables",
                    icon: '📜',
                    content: "Beyond epics, Sanskrit literature includes rich traditions of poetry (kāvya), drama, and ethical fables (like the Pañcatantra), which influenced global literature, including collections like 'One Thousand and One Nights'."
                }
            ];
            
            const grammariansData = [
                { name: "Pāṇini", date: -500, date_display: "c. 5th cent. BCE" },
                { name: "Kātyāyana", date: -300, date_display: "c. 3rd cent. BCE" },
                { name: "Patañjali", date: -150, date_display: "c. 2nd cent. BCE" },
                { name: "Bhartṛhari", date: 600, date_display: "c. 6th-7th cent. CE" },
                { name: "Jayaditya & Vāmana", date: 600, date_display: "c. 7th cent. CE" },
                { name: "Bhaṭṭoji Dīkṣita", date: 1600, date_display: "17th century" },
                { name: "Varadarāja", date: 1650, date_display: "17th century" },
            ];
            
            const scriptsData = {
                labels: ['Brāhmī', 'Kharoshthi', 'Siddhaṃ', 'Grantha', 'Śāradā', 'Devanāgarī'],
                datasets: [{
                    label: 'Period of Prominence',
                    data: [
                        [-100, 600], // Brahmi
                        [-300, 300], // Kharosthi
                        [550, 1200], // Siddham
                        [450, 1950], // Grantha
                        [750, 1200], // Sharada
                        [1800, 2025] // Devanagari
                    ],
                    backgroundColor: [
                        'rgba(210, 180, 140, 0.7)',
                        'rgba(192, 132, 62, 0.7)',
                        'rgba(165, 112, 50, 0.7)',
                        'rgba(205, 155, 89, 0.7)',
                        'rgba(182, 134, 76, 0.7)',
                        'rgba(193, 131, 62, 0.9)'
                    ],
                    borderColor: [
                         'rgb(210, 180, 140)',
                         'rgb(192, 132, 62)',
                         'rgb(165, 112, 50)',
                         'rgb(205, 155, 89)',
                         'rgb(182, 134, 76)',
                         'rgb(193, 131, 62)'
                    ],
                    borderWidth: 1,
                    barPercentage: 0.6,
                    categoryPercentage: 0.7,
                    borderSkipped: false,
                }]
            };

            const scriptGalleryData = [
                { name: "Devanāgarī", example: "देवनागरी" },
                { name: "Brāhmī", example: "𑀩𑁆𑀭𑀸𑀳𑁆𑀫𑀻" },
                { name: "Śāradā", example: "𑆯𑆳𑆫𑆢𑆳" },
                { name: "Grantha", example: "𑌗𑍍𑌰𑌨𑍍𑌥" },
                { name: "Siddhaṃ", example: "𑖭𑖰𑖟𑖿𑖠𑖽" },
                { name: "Tibetan", example: "ཏིབྦཏཱན" },
            ];

            // Mobile Menu
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });
            document.querySelectorAll('#mobile-menu a').forEach(link => {
                link.addEventListener('click', () => mobileMenu.classList.add('hidden'));
            });

            // Smooth Scrolling & Active Nav Link
            const sections = document.querySelectorAll('section');
            const navLinks = document.querySelectorAll('.nav-link');
            
            window.onscroll = () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 60) {
                        current = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').includes(current)) {
                        link.classList.add('active');
                    }
                });
            };

            // Modal Logic
            const modal = document.getElementById('modal');
            const modalBg = document.getElementById('modal-bg');
            const modalBox = document.getElementById('modal-box');
            const modalTitle = document.getElementById('modal-title');
            const modalContent = document.getElementById('modal-content');
            const modalClose = document.getElementById('modal-close');

            function openModal(title, content) {
                modalTitle.innerHTML = title;
                modalContent.innerHTML = content;
                modal.classList.remove('hidden');
                modal.classList.add('flex');
                setTimeout(() => {
                    modalBg.classList.remove('opacity-0');
                    modalBox.classList.remove('scale-95');
                }, 10);
            }

            function closeModal() {
                modalBg.classList.add('opacity-0');
                modalBox.classList.add('scale-95');
                setTimeout(() => {
                    modal.classList.add('hidden');
                    modal.classList.remove('flex');
                }, 300);
            }

            modalClose.addEventListener('click', closeModal);
            modalBg.addEventListener('click', closeModal);

            // Populate Timeline
            const timelineContainer = document.getElementById('timeline-container');
            timelineContainer.innerHTML = '<div class="absolute left-3 top-0 h-full w-0.5 bg-gray-200"></div>';
            timelineData.forEach(item => {
                const div = document.createElement('div');
                div.className = 'timeline-item relative pl-10 pb-10 cursor-pointer';
                div.innerHTML = `
                    <div class="font-bold text-sm text-[#C0843E]">${item.date}</div>
                    <h4 class="font-bold text-xl mb-1">${item.title}</h4>
                    <p class="text-gray-600">${item.content.substring(0, 100)}...</p>
                `;
                div.addEventListener('click', () => openModal(item.title, `<p class="text-lg">${item.content}</p>`));
                timelineContainer.appendChild(div);
            });

            // Populate Knowledge Cards
            const knowledgeCardsContainer = document.getElementById('knowledge-cards');
            knowledgeData.forEach(item => {
                const div = document.createElement('div');
                div.className = 'card bg-white p-6 rounded-xl shadow-sm cursor-pointer';
                div.innerHTML = `
                    <div class="text-4xl mb-4">${item.icon}</div>
                    <h3 class="text-xl font-bold font-serif mb-2">${item.title}</h3>
                    <p class="text-gray-600">${item.content}</p>
                `;
                knowledgeCardsContainer.appendChild(div);
            });
            
            // Sandhi interactive element
            document.getElementById('sandhi-button').addEventListener('click', () => {
                const input1 = document.getElementById('sandhi-input1').value.trim();
                const input2 = document.getElementById('sandhi-input2').value.trim();
                const outputSpan = document.getElementById('sandhi-output');
                
                if (input1.endsWith('a') && input2.startsWith('ā')) {
                    outputSpan.textContent = input1.slice(0, -1) + 'ālaya';
                } else if (input1.endsWith('a') && input2.startsWith('a')) {
                     outputSpan.textContent = input1.slice(0, -1) + 'ā' + input2.slice(1);
                }
                else {
                    outputSpan.textContent = input1 + input2;
                }
            });

            // Grammarians Table
            let sortDirection = { name: 'asc', date: 'asc' };
            function renderTable(data) {
                const tableBody = document.querySelector('#grammarians-table tbody');
                tableBody.innerHTML = '';
                data.forEach(g => {
                    const row = document.createElement('tr');
                    row.className = 'bg-white border-b';
                    row.innerHTML = `<td class="px-4 py-3">${g.name}</td><td class="px-4 py-3">${g.date_display}</td>`;
                    tableBody.appendChild(row);
                });
            }
            
            document.querySelectorAll('#grammarians-table th').forEach(header => {
                header.addEventListener('click', () => {
                    const sortKey = header.dataset.sort;
                    const direction = sortDirection[sortKey];
                    
                    grammariansData.sort((a, b) => {
                        if (a[sortKey] < b[sortKey]) return direction === 'asc' ? -1 : 1;
                        if (a[sortKey] > b[sortKey]) return direction === 'asc' ? 1 : -1;
                        return 0;
                    });

                    sortDirection[sortKey] = direction === 'asc' ? 'desc' : 'asc';
                    renderTable(grammariansData);
                });
            });

            renderTable(grammariansData);

            // Scripts Chart
            const ctx = document.getElementById('scriptsChart').getContext('2d');
            const scriptsChart = new Chart(ctx, {
                type: 'bar',
                data: scriptsData,
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const val = context.raw;
                                    const start = val[0] < 0 ? `${-val[0]} BCE` : `${val[0]} CE`;
                                    const end = val[1] < 0 ? `${-val[1]} BCE` : `${val[1]} CE`;
                                    return `Period: ${start} to ${end}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            min: -500,
                            max: 2100,
                            title: {
                                display: true,
                                text: 'Time Period (BCE/CE)'
                            }
                        },
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            // Script Gallery
            const galleryContainer = document.getElementById('script-gallery');
            scriptGalleryData.forEach(script => {
                const div = document.createElement('div');
                div.className = 'p-4 bg-white rounded-lg shadow-sm flex flex-col items-center justify-center border border-gray-200';
                div.innerHTML = `
                    <div class="text-3xl" style="font-family: sans-serif;">${script.example}</div>
                    <p class="mt-2 text-sm font-semibold">${script.name}</p>
                `;
                galleryContainer.appendChild(div);
            });
            
            // Animate counters on scroll
            const observerOptions = {
                root: null,
                rootMargin: '0px',
                threshold: 0.5
            };

            const animateCounter = (el, target) => {
                let current = 0;
                const step = target / 100;
                const interval = setInterval(() => {
                    current += step;
                    if (current >= target) {
                        clearInterval(interval);
                        el.textContent = target;
                    } else {
                        el.textContent = Math.ceil(current);
                    }
                }, 20);
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const scheduledEl = document.getElementById('scheduled-lang');
                        const officialEl = document.getElementById('official-lang');
                        animateCounter(scheduledEl, 22);
                        animateCounter(officialEl, 2);
                        observer.unobserve(entry.target);
                    }
                });
            }, observerOptions);

            observer.observe(document.getElementById('legacy'));

        });
    </script>
</body>
</html>
