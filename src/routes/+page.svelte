<script lang="ts">
  import { onMount } from 'svelte';
  
  let mobileMenuOpen = $state(false);
  
  function toggleMobileMenu() {
    mobileMenuOpen = !mobileMenuOpen;
  }
  
  function closeMobileMenu() {
    mobileMenuOpen = false;
  }
  
  onMount(() => {
    // Initialize slider
    const slides = document.querySelectorAll('.slide');
    let currentSlide = 0;
    
    function showSlide(index: number) {
      slides.forEach((slide, i) => {
        slide.classList.toggle('active', i === index);
      });
    }
    
    function nextSlide() {
      currentSlide = (currentSlide + 1) % slides.length;
      showSlide(currentSlide);
    }
    
    // Auto-advance slides every 5 seconds
    const slideInterval = setInterval(nextSlide, 5000);
    
    // Smooth scroll for anchor links
    document.querySelectorAll('a[href^="#"]').forEach((anchor) => {
      anchor.addEventListener('click', function (e: Event) {
        e.preventDefault();
        const href = (anchor as HTMLAnchorElement).getAttribute('href');
        if (href) {
          const target = document.querySelector(href);
          if (target) {
            target.scrollIntoView({
              behavior: 'smooth',
              block: 'start'
            });
            // Close mobile menu if open
            mobileMenuOpen = false;
          }
        }
      });
    });
    
    // Close mobile menu on scroll
    function handleScrollClose() {
      if (mobileMenuOpen) {
        mobileMenuOpen = false;
      }
    }
    
    window.addEventListener('scroll', handleScrollClose);
    
    // Trigger animations on scroll
    const observerOptions = {
      threshold: 0.1,
      rootMargin: '0px 0px -50px 0px'
    };
    
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('animate-fadeInUp');
          const htmlEl = entry.target as HTMLElement;
          htmlEl.style.opacity = '1';
        }
      });
    }, observerOptions);
    
    document.querySelectorAll('.animate-fadeInUp').forEach(el => {
      observer.observe(el);
    });
    
    return () => {
      clearInterval(slideInterval);
      window.removeEventListener('scroll', handleScrollClose);
    };
  });
</script>

<svelte:head>
  <title>Permits & More - Expert Permit Processing & Inspection Services</title>
  <meta name="description" content="Professional permit processing and inspection coordination services for construction projects throughout Southern California." />
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
  <!-- Link UX Pilot CSS -->
  <link rel="stylesheet" href="/css/style.css">
</svelte:head>

<div class="bg-white">
    <header id="header"
      class="fixed top-0 left-0 right-0 z-50 transition-all duration-300 bg-[#1e3a8a]/50 backdrop-blur-sm">
      <div class="max-w-[1440px] mx-auto px-4 md:px-8 py-3 md:py-4">
        <div class="flex items-center justify-between">
          <div class="flex items-center"><img
              src="https://i0.wp.com/permitsandmore.com/wp-content/uploads/2016/06/cropped-logo-1.png?fit=263%2C60&amp;ssl=1"
              alt="Permits &amp; More Logo" class="h-12 md:h-16 w-auto"></div>
          <!-- Desktop Navigation -->
          <nav class="hidden lg:flex items-center space-x-6 xl:space-x-8">
            <a href="#home" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">Home</a>
            <a href="#services" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">Services</a>
            <a href="#about" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">About</a>
            <a href="#process" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">Process</a>
            <a href="#testimonials" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">Testimonials</a>
            <a href="#contact" onclick={closeMobileMenu}
              class="nav-link text-white font-medium text-sm uppercase tracking-wide">Contact</a>
            <button
              class="bg-[#3b82f6] hover:bg-[#2563eb] text-white px-6 xl:px-8 py-2.5 xl:py-3 rounded-full font-semibold text-sm xl:text-base transition-all duration-300 transform hover:scale-105 shadow-lg">
              Get Started
            </button>
          </nav>
          <!-- Mobile Menu Button -->
          <button
            onclick={toggleMobileMenu}
            class="lg:hidden text-white p-2 focus:outline-none"
            aria-label="Toggle menu"
            aria-expanded={mobileMenuOpen}>
            {#if mobileMenuOpen}
              <i class="fa-solid fa-times text-2xl"></i>
            {:else}
              <i class="fa-solid fa-bars text-2xl"></i>
            {/if}
          </button>
        </div>
        <!-- Mobile Navigation Menu -->
        {#if mobileMenuOpen}
          <nav class="lg:hidden mt-4 pb-4 border-t border-white/20 pt-4">
            <div class="flex flex-col space-y-4">
              <a href="#home" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">Home</a>
              <a href="#services" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">Services</a>
              <a href="#about" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">About</a>
              <a href="#process" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">Process</a>
              <a href="#testimonials" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">Testimonials</a>
              <a href="#contact" onclick={closeMobileMenu}
                class="nav-link text-white font-medium text-base uppercase tracking-wide py-2">Contact</a>
              <button
                onclick={closeMobileMenu}
                class="bg-[#3b82f6] hover:bg-[#2563eb] text-white px-6 py-3 rounded-full font-semibold text-base transition-all duration-300 shadow-lg w-full mt-2">
                Get Started
              </button>
            </div>
          </nav>
        {/if}
      </div>
    </header>
    <section id="hero-section" class="relative h-[500px] md:h-[600px] lg:h-[800px] slider-container">
      <div class="slide active"><img
          src="https://storage.googleapis.com/uxpilot-auth.appspot.com/49b2095347-2bb481764220134c1869.png"
          alt="modern construction site with building permits and blueprints, professional architecture photography, premium quality, wide angle"
          class="w-full h-full object-cover">
        <div class="absolute inset-0 gradient-overlay"></div>
      </div>
      <div class="slide"><img
          src="https://storage.googleapis.com/uxpilot-auth.appspot.com/928b4fb573-6ac86857e21980919a65.png"
          alt="commercial building inspection with professional inspector reviewing permits, high-end architectural photography"
          class="w-full h-full object-cover">
        <div class="absolute inset-0 gradient-overlay"></div>
      </div>
      <div class="slide"><img
          src="https://storage.googleapis.com/uxpilot-auth.appspot.com/f2f35aba59-e83f97eea49778969d0d.png"
          alt="residential construction project with permits documentation, modern home building, professional photography"
          class="w-full h-full object-cover">
        <div class="absolute inset-0 gradient-overlay"></div>
      </div>
      <div class="absolute inset-0 flex items-center justify-center">
        <div class="text-center text-white max-w-4xl px-8">
          <h1
            class="font-display text-3xl sm:text-4xl md:text-5xl lg:text-6xl xl:text-7xl font-bold mb-4 md:mb-6 animate-fadeInUp opacity-0 px-4">
            Expert Permit Processing &amp; Inspection Services
          </h1>
          <p
            class="text-base sm:text-lg md:text-xl lg:text-2xl mb-6 md:mb-8 animate-fadeInUp opacity-0 delay-200 font-light px-4">
            Streamlining Your Construction Projects with Professional Compliance
            Solutions
          </p><button
            class="hero-cta-button bg-[#3b82f6] hover:bg-[#2563eb] text-white px-6 sm:px-8 md:px-12 py-3 md:py-4 rounded-full text-sm sm:text-base md:text-lg font-semibold transform hover:scale-105 shadow-2xl animate-fadeInUp opacity-0 delay-400">
            Request a Consultation
          </button>
        </div>
      </div>
    </section>
    <section id="services" class="py-12 md:py-16 lg:py-24 bg-gray-50">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="text-center mb-16">
          <h2 class="font-display text-3xl sm:text-4xl md:text-5xl font-bold text-gray-900 mb-4">Our
            Comprehensive Services</h2>
          <p class="text-base sm:text-lg md:text-xl text-gray-600 max-w-3xl mx-auto px-4">
            From permit acquisition to final inspection, we handle every aspect
            of your project's compliance needs
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div id="service-card-1"
            class="bg-white rounded-2xl shadow-xl p-8 hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2">
            <div
              class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
              <i class="fa-solid fa-file-contract text-3xl text-[#1e3a8a]"></i>
            </div>
            <h3 class="font-display text-2xl font-bold text-gray-900 mb-4">
              Permit Processing</h3>
            <p class="text-gray-600 mb-6 leading-relaxed">
              Expert navigation through complex permit applications for
              residential and commercial projects. We handle all documentation,
              submissions, and follow-ups to ensure timely approvals.
            </p>
            <ul class="space-y-3 mb-6">
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Building Permits</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Electrical Permits</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Plumbing Permits</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Mechanical Permits</span></li>
            </ul><a href="#"
              class="text-secondary font-semibold hover:text-accent transition-colors">
              Learn More <i class="fa-solid fa-arrow-right ml-2"></i></a>
          </div>
          <div id="service-card-2"
            class="bg-white rounded-2xl shadow-xl p-8 hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2">
            <div
              class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
              <i class="fa-solid fa-clipboard-check text-3xl text-[#1e3a8a]"></i>
            </div>
            <h3 class="font-display text-2xl font-bold text-gray-900 mb-4">
              Inspection Coordination</h3>
            <p class="text-gray-600 mb-6 leading-relaxed">
              Comprehensive inspection scheduling and coordination services
              ensuring your project meets all code requirements and passes
              inspections on the first attempt.
            </p>
            <ul class="space-y-3 mb-6">
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Pre-Inspection Reviews</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Inspection Scheduling</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">On-Site Representation</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Final Sign-Off</span></li>
            </ul><a href="#"
              class="text-secondary font-semibold hover:text-accent transition-colors">
              Learn More <i class="fa-solid fa-arrow-right ml-2"></i></a>
          </div>
          <div id="service-card-3"
            class="bg-white rounded-2xl shadow-xl p-8 hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2">
            <div
              class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
              <i class="fa-solid fa-balance-scale text-3xl text-[#1e3a8a]"></i>
            </div>
            <h3 class="font-display text-2xl font-bold text-gray-900 mb-4">
              Compliance Support</h3>
            <p class="text-gray-600 mb-6 leading-relaxed">
              Stay ahead of regulatory requirements with our expert compliance
              support services. We keep you informed of code changes and ensure
              full adherence to local regulations.
            </p>
            <ul class="space-y-3 mb-6">
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Code Compliance Review</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Zoning Analysis</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Regulatory Updates</span></li>
              <li class="flex items-start"><i
                  class="fa-solid fa-check text-secondary mr-3 mt-1"></i><span
                  class="text-gray-700">Documentation Management</span></li>
            </ul><a href="#"
              class="text-secondary font-semibold hover:text-accent transition-colors">
              Learn More <i class="fa-solid fa-arrow-right ml-2"></i></a>
          </div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-8">
          <div id="service-card-4"
            class="bg-white rounded-2xl shadow-xl p-8 hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2">
            <div
              class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
              <i class="fa-solid fa-building text-3xl text-[#1e3a8a]"></i></div>
            <h3 class="font-display text-2xl font-bold text-gray-900 mb-4">
              Commercial Projects</h3>
            <p class="text-gray-600 mb-6 leading-relaxed">
              Specialized services for commercial construction projects
              including office buildings, retail spaces, restaurants, and
              industrial facilities. We understand the unique challenges of
              commercial permitting.
            </p>
            <div class="grid grid-cols-2 gap-4">
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-store text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Retail Spaces</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-utensils text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Restaurants</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-briefcase text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Office Buildings
                </p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-industry text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Industrial</p>
              </div>
            </div>
          </div>
          <div id="service-card-5"
            class="bg-white rounded-2xl shadow-xl p-8 hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2">
            <div
              class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mb-6">
              <i class="fa-solid fa-home text-3xl text-[#1e3a8a]"></i></div>
            <h3 class="font-display text-2xl font-bold text-gray-900 mb-4">
              Residential Projects</h3>
            <p class="text-gray-600 mb-6 leading-relaxed">
              Comprehensive permit and inspection services for residential
              construction, remodeling, and additions. From single-family homes
              to multi-unit developments, we've got you covered.
            </p>
            <div class="grid grid-cols-2 gap-4">
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-house-user text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">New Construction
                </p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-hammer text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Remodeling</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-plus-square text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Additions</p>
              </div>
              <div class="bg-gray-50 p-4 rounded-lg"><i
                  class="fa-solid fa-solar-panel text-[#1e3a8a] text-2xl mb-2"></i>
                <p class="text-sm font-semibold text-gray-700">Solar Permits</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="about" class="py-12 md:py-16 lg:py-24 bg-white">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-16 items-center">
          <div>
            <div class="h-[500px] overflow-hidden rounded-2xl shadow-2xl"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/fa9c7a6e86-05f45ac384674ed211af.png"
                alt="professional team reviewing construction permits and blueprints in modern office, business photography, high quality"
                class="w-full h-full object-cover"></div>
          </div>
          <div>
            <h2 class="font-display text-3xl sm:text-4xl md:text-5xl font-bold text-gray-900 mb-4 md:mb-6">Why
              Choose Permits &amp; More</h2>
            <p class="text-base sm:text-lg md:text-xl text-gray-600 mb-6 md:mb-8 leading-relaxed">
              With years of experience in the construction and permitting
              industry, we've built our reputation on delivering exceptional
              service and ensuring your projects stay on track and compliant.
            </p>
            <div class="space-y-6">
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-award text-[#1e3a8a] text-xl"></i></div>
                <div>
                  <h3 class="text-xl font-bold text-gray-900 mb-2">Industry
                    Expertise</h3>
                  <p class="text-gray-600">Decades of combined experience in
                    construction permitting and compliance across residential
                    and commercial projects.</p>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-clock text-[#1e3a8a] text-xl"></i></div>
                <div>
                  <h3 class="text-xl font-bold text-gray-900 mb-2">Fast
                    Turnaround</h3>
                  <p class="text-gray-600">We expedite the permit process,
                    reducing delays and keeping your construction timeline on
                    schedule.</p>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-handshake text-[#1e3a8a] text-xl"></i>
                </div>
                <div>
                  <h3 class="text-xl font-bold text-gray-900 mb-2">Personalized
                    Service</h3>
                  <p class="text-gray-600">Dedicated account managers who
                    understand your specific project needs and provide tailored
                    solutions.</p>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-shield-alt text-[#1e3a8a] text-xl"></i>
                </div>
                <div>
                  <h3 class="text-xl font-bold text-gray-900 mb-2">Compliance
                    Guarantee</h3>
                  <p class="text-gray-600">Our thorough review process ensures
                    all permits and inspections meet local, state, and federal
                    requirements.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="process"
      class="py-12 md:py-16 lg:py-24 bg-[#1e3a8a] text-white">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="text-center mb-16">
          <h2 class="font-display text-3xl sm:text-4xl md:text-5xl font-bold mb-4">Our Streamlined
            Process</h2>
          <p class="text-base sm:text-lg md:text-xl text-blue-100 max-w-3xl mx-auto px-4">
            A proven methodology that ensures efficient permit processing and
            successful project completion
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
          <div id="process-step-1" class="text-center">
            <div
              class="w-24 h-24 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-xl">
              <span class="text-4xl font-bold text-[#3b82f6]">1</span></div>
            <h3 class="text-2xl font-bold mb-4">Initial Consultation</h3>
            <p class="text-blue-100 leading-relaxed">
              We review your project plans, discuss requirements, and identify
              all necessary permits and inspections needed for your construction
              project.
            </p>
          </div>
          <div id="process-step-2" class="text-center">
            <div
              class="w-24 h-24 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-xl">
              <span class="text-4xl font-bold text-[#3b82f6]">2</span></div>
            <h3 class="text-2xl font-bold mb-4">Documentation Prep</h3>
            <p class="text-blue-100 leading-relaxed">
              Our team prepares all required documentation, drawings, and
              applications ensuring accuracy and completeness for submission to
              authorities.
            </p>
          </div>
          <div id="process-step-3" class="text-center">
            <div
              class="w-24 h-24 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-xl">
              <span class="text-4xl font-bold text-[#3b82f6]">3</span></div>
            <h3 class="text-2xl font-bold mb-4">Permit Submission</h3>
            <p class="text-blue-100 leading-relaxed">
              We submit applications to the appropriate agencies, track
              progress, and handle all communications with building departments
              and inspectors.
            </p>
          </div>
          <div id="process-step-4" class="text-center">
            <div
              class="w-24 h-24 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-xl">
              <span class="text-4xl font-bold text-[#3b82f6]">4</span></div>
            <h3 class="text-2xl font-bold mb-4">Inspection &amp; Approval</h3>
            <p class="text-blue-100 leading-relaxed">
              We coordinate all inspections, provide on-site representation if
              needed, and ensure successful completion and final sign-off of
              your project.
            </p>
          </div>
        </div>
        <div class="mt-16 bg-white/10 backdrop-blur-sm rounded-2xl p-12">
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
            <div>
              <div class="text-5xl font-bold mb-2">500+</div>
              <p class="text-blue-100 text-lg">Projects Completed</p>
            </div>
            <div>
              <div class="text-5xl font-bold mb-2">98%</div>
              <p class="text-blue-100 text-lg">First-Time Approval Rate</p>
            </div>
            <div>
              <div class="text-5xl font-bold mb-2">15+</div>
              <p class="text-blue-100 text-lg">Years of Experience</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="service-areas" class="py-12 md:py-16 lg:py-24 bg-gray-50">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="text-center mb-16">
          <h2 class="font-display text-5xl font-bold text-gray-900 mb-4">Service
            Areas</h2>
          <p class="text-xl text-gray-600 max-w-3xl mx-auto">
            Proudly serving San Diego County and surrounding areas with
            comprehensive permit and inspection services
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <div class="bg-white rounded-2xl shadow-xl overflow-hidden">
            <div class="h-[300px] overflow-hidden"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/685ed0c7a3-a1a6ee1b1ffb6486a9af.png"
                alt="San Diego California skyline aerial view, beautiful city landscape photography"
                class="w-full h-full object-cover"></div>
            <div class="p-8">
              <h3 class="font-display text-3xl font-bold text-gray-900 mb-4">San
                Diego County</h3>
              <p class="text-gray-600 mb-6 leading-relaxed">
                Comprehensive coverage throughout San Diego County including all
                cities and unincorporated areas. Our local expertise ensures
                smooth navigation of county-specific requirements.
              </p>
              <div class="grid grid-cols-2 gap-4">
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">Downtown San Diego</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">North County</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">East County</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">South Bay</span></div>
              </div>
            </div>
          </div>
          <div class="bg-white rounded-2xl shadow-xl overflow-hidden">
            <div class="h-[300px] overflow-hidden"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/0f42743cc1-5b43c0799e7e610bf657.png"
                alt="Southern California coastal cities landscape, professional photography"
                class="w-full h-full object-cover"></div>
            <div class="p-8">
              <h3 class="font-display text-3xl font-bold text-gray-900 mb-4">
                Surrounding Areas</h3>
              <p class="text-gray-600 mb-6 leading-relaxed">
                Extended service coverage to neighboring counties and regions.
                We maintain strong relationships with building departments
                across Southern California.
              </p>
              <div class="grid grid-cols-2 gap-4">
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">Riverside County</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">Orange County</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">Imperial County</span></div>
                <div class="flex items-center"><i
                    class="fa-solid fa-map-marker-alt text-secondary mr-2"></i><span
                    class="text-gray-700">Los Angeles County</span></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section id="testimonials" class="py-12 md:py-16 lg:py-24 bg-white">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="text-center mb-16">
          <h2 class="font-display text-5xl font-bold text-gray-900 mb-4">What
            Our Clients Say</h2>
          <p class="text-xl text-gray-600 max-w-3xl mx-auto">
            Don't just take our word for it - hear from contractors, builders,
            and property owners who trust us with their projects
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div id="testimonial-1"
            class="bg-gray-50 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300">
            <div class="flex items-center mb-6"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/avatars/avatar-2.jpg"
                alt="Client" class="w-16 h-16 rounded-full mr-4">
              <div>
                <h4 class="font-bold text-gray-900">Michael Rodriguez</h4>
                <p class="text-gray-600 text-sm">General Contractor</p>
              </div>
            </div>
            <div class="flex mb-4"><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i></div>
            <p class="text-gray-700 leading-relaxed italic">
              "Permits &amp; More has been instrumental in keeping our
              commercial projects on schedule. Their expertise in navigating
              complex permitting processes has saved us countless hours and
              headaches. Highly recommended!"
            </p>
          </div>
          <div id="testimonial-2"
            class="bg-gray-50 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300">
            <div class="flex items-center mb-6"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/avatars/avatar-5.jpg"
                alt="Client" class="w-16 h-16 rounded-full mr-4">
              <div>
                <h4 class="font-bold text-gray-900">Jennifer Thompson</h4>
                <p class="text-gray-600 text-sm">Property Developer</p>
              </div>
            </div>
            <div class="flex mb-4"><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i></div>
            <p class="text-gray-700 leading-relaxed italic">
              "Working with Permits &amp; More has been a game-changer for our
              development projects. Their attention to detail and proactive
              communication ensure we never miss a deadline. They're now our
              go-to for all permitting needs."
            </p>
          </div>
          <div id="testimonial-3"
            class="bg-gray-50 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300">
            <div class="flex items-center mb-6"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/avatars/avatar-8.jpg"
                alt="Client" class="w-16 h-16 rounded-full mr-4">
              <div>
                <h4 class="font-bold text-gray-900">David Chen</h4>
                <p class="text-gray-600 text-sm">Residential Builder</p>
              </div>
            </div>
            <div class="flex mb-4"><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i></div>
            <p class="text-gray-700 leading-relaxed italic">
              "The team at Permits &amp; More is incredibly knowledgeable and
              professional. They handled all our residential permits
              efficiently, and their inspection coordination service is
              top-notch. We couldn't be happier with their service."
            </p>
          </div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-8">
          <div id="testimonial-4"
            class="bg-gray-50 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300">
            <div class="flex items-center mb-6"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/avatars/avatar-6.jpg"
                alt="Client" class="w-16 h-16 rounded-full mr-4">
              <div>
                <h4 class="font-bold text-gray-900">Sarah Martinez</h4>
                <p class="text-gray-600 text-sm">Restaurant Owner</p>
              </div>
            </div>
            <div class="flex mb-4"><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i></div>
            <p class="text-gray-700 leading-relaxed italic">
              "Opening a restaurant involves so many permits and inspections.
              Permits &amp; More made the entire process seamless. They knew
              exactly what was needed and handled everything professionally. Our
              grand opening happened right on schedule!"
            </p>
          </div>
          <div id="testimonial-5"
            class="bg-gray-50 rounded-2xl p-8 shadow-lg hover:shadow-xl transition-all duration-300">
            <div class="flex items-center mb-6"><img
                src="https://storage.googleapis.com/uxpilot-auth.appspot.com/avatars/avatar-4.jpg"
                alt="Client" class="w-16 h-16 rounded-full mr-4">
              <div>
                <h4 class="font-bold text-gray-900">Robert Johnson</h4>
                <p class="text-gray-600 text-sm">Commercial Property Manager</p>
              </div>
            </div>
            <div class="flex mb-4"><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i><i
                class="fa-solid fa-star text-yellow-400"></i></div>
            <p class="text-gray-700 leading-relaxed italic">
              "Managing multiple properties means dealing with various permits
              and compliance issues. Permits &amp; More has become an invaluable
              partner, handling everything from tenant improvements to building
              upgrades with exceptional expertise."
            </p>
          </div>
        </div>
      </div>
    </section>
    <section id="faq" class="py-12 md:py-16 lg:py-24 bg-gray-50">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="text-center mb-16">
          <h2 class="font-display text-5xl font-bold text-gray-900 mb-4">
            Frequently Asked Questions</h2>
          <p class="text-xl text-gray-600 max-w-3xl mx-auto">
            Find answers to common questions about our permit processing and
            inspection services
          </p>
        </div>
        <div class="max-w-4xl mx-auto space-y-6">
          <div id="faq-1" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              How long does the permit process typically take?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              The timeline varies depending on project complexity and
              jurisdiction. Simple residential permits can take 2-4 weeks, while
              complex commercial projects may require 6-12 weeks. We expedite
              the process by ensuring complete and accurate submissions from the
              start.
            </p>
          </div>
          <div id="faq-2" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              What information do you need to get started?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              We'll need your project plans, property information, scope of work
              details, and any existing documentation. During our initial
              consultation, we'll provide a complete checklist of required
              materials specific to your project.
            </p>
          </div>
          <div id="faq-3" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              Do you handle inspections for all trade types?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              Yes, we coordinate all types of inspections including building,
              electrical, plumbing, mechanical, fire safety, and specialty
              inspections. Our team has relationships with inspectors across all
              disciplines.
            </p>
          </div>
          <div id="faq-4" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              What if my project fails an inspection?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              We conduct pre-inspection reviews to minimize this risk. If issues
              arise, we work with you and the inspector to identify corrections
              needed and coordinate re-inspection once remedies are complete.
            </p>
          </div>
          <div id="faq-5" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              Can you help with projects outside San Diego County?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              Yes, we service surrounding counties including Riverside, Orange,
              Imperial, and Los Angeles. Our network and expertise extend
              throughout Southern California.
            </p>
          </div>
          <div id="faq-6" class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-4 flex items-center">
              <i class="fa-solid fa-question-circle text-secondary mr-3"></i>
              How much do your services cost?
            </h3>
            <p class="text-gray-600 leading-relaxed ml-9">
              Our fees vary based on project scope, complexity, and location. We
              provide transparent, upfront pricing after reviewing your project
              details. Contact us for a free consultation and quote.
            </p>
          </div>
        </div>
      </div>
    </section>
    <section id="contact" class="py-12 md:py-16 lg:py-24 bg-white">
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 md:px-8">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-16">
          <div>
            <h2 class="font-display text-3xl sm:text-4xl md:text-5xl font-bold text-gray-900 mb-4 md:mb-6">Get
              In Touch</h2>
            <p class="text-base sm:text-lg md:text-xl text-gray-600 mb-6 md:mb-8 leading-relaxed">
              Ready to start your project? Contact us today for a free
              consultation. Our team is here to answer your questions and
              provide expert guidance.
            </p>
            <div class="space-y-6">
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-phone text-[#1e3a8a] text-xl"></i></div>
                <div>
                  <h3 class="font-bold text-gray-900 mb-1">Phone</h3><a
                    href="tel:619-323-4048"
                    class="text-[#1e3a8a] hover:text-[#1e40af] transition-colors text-lg">619-323-4048</a>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-envelope text-[#1e3a8a] text-xl"></i>
                </div>
                <div>
                  <h3 class="font-bold text-gray-900 mb-1">Email</h3><a
                    href="mailto:info@permitsandmore.com"
                    class="text-[#1e3a8a] hover:text-[#1e40af] transition-colors text-lg">info@permitsandmore.com</a>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i
                    class="fa-solid fa-map-marker-alt text-[#1e3a8a] text-xl"></i>
                </div>
                <div>
                  <h3 class="font-bold text-gray-900 mb-1">Address</h3>
                  <p class="text-gray-600 text-lg">101 West Broadway<br>Suite
                    300<br>San Diego CA 92101</p>
                </div>
              </div>
              <div class="flex items-start">
                <div
                  class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                  <i class="fa-solid fa-clock text-[#1e3a8a] text-xl"></i></div>
                <div>
                  <h3 class="font-bold text-gray-900 mb-1">Business Hours</h3>
                  <p class="text-gray-600">Monday - Friday: 8:00 AM - 6:00
                    PM<br>Saturday: 9:00 AM - 2:00 PM<br>Sunday: Closed</p>
                </div>
              </div>
            </div>
          </div>
          <div id="contact-form" class="bg-gray-50 rounded-2xl p-8 shadow-xl">
            <h3 class="text-2xl font-bold text-gray-900 mb-6">Send Us a Message
            </h3>
            <form class="space-y-6">
              <div><label class="block text-gray-700 font-semibold mb-2">Full
                  Name *</label><input type="text" placeholder="John Doe"
                  class="w-full px-4 py-3 rounded-lg border border-gray-300 text-gray-700 placeholder-gray-500 focus:border-secondary focus:ring-2 focus:ring-secondary/20 outline-none transition-all">
              </div>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div><label class="block text-gray-700 font-semibold mb-2">Email
                    *</label><input type="email" placeholder="john@example.com"
                    class="w-full px-4 py-3 rounded-lg border border-gray-300 text-gray-700 placeholder-gray-500 focus:border-secondary focus:ring-2 focus:ring-secondary/20 outline-none transition-all">
                </div>
                <div><label class="block text-gray-700 font-semibold mb-2">Phone
                    *</label><input type="tel" placeholder="(619) 555-0123"
                    class="w-full px-4 py-3 rounded-lg border border-gray-300 text-gray-700 placeholder-gray-500 focus:border-secondary focus:ring-2 focus:ring-secondary/20 outline-none transition-all">
                </div>
              </div>
              <div><label class="block text-gray-700 font-semibold mb-2">Project
                  Type *</label><select
                  class="w-full px-4 py-3 rounded-lg border border-gray-300 text-gray-700 focus:border-secondary focus:ring-2 focus:ring-secondary/20 outline-none transition-all">
                  <option>Select Project Type</option>
                  <option>Residential New Construction</option>
                  <option>Residential Remodel</option>
                  <option>Commercial New Construction</option>
                  <option>Commercial Tenant Improvement</option>
                  <option>Industrial</option>
                  <option>Other</option>
                </select></div>
              <div><label class="block text-gray-700 font-semibold mb-2">Message
                  *</label><textarea rows="5" placeholder="Tell us about your project..." class="w-full px-4 py-3 rounded-lg border border-gray-300 text-gray-700 placeholder-gray-500 focus:border-secondary focus:ring-2 focus:ring-secondary/20 outline-none transition-all"></textarea>
              </div><button type="submit"
                class="w-full bg-[#3b82f6] hover:bg-[#2563eb] text-white py-4 rounded-lg font-semibold text-lg transition-all duration-300 transform hover:scale-105 shadow-lg">
                Send Message
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
    <section id="cta-highlight" class="relative h-[400px] md:h-[500px] overflow-hidden"><img
        src="https://storage.googleapis.com/uxpilot-auth.appspot.com/6f736a88e0-4cc6e3756abb280cf77c.png"
        alt="modern construction site at golden hour with cranes and buildings under construction, professional architecture photography, cinematic lighting"
        class="w-full h-full object-cover">
      <div
        class="absolute inset-0 bg-gradient-to-r from-primary/90 to-blue-900/90">
      </div>
      <div class="absolute inset-0 flex items-center justify-center">
        <div class="text-center text-white max-w-4xl px-8">
          <h2 class="font-display text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold mb-4 md:mb-6 px-4">
            Ready to Streamline Your Permit Process?
          </h2>
          <p class="text-base sm:text-lg md:text-xl lg:text-2xl mb-6 md:mb-8 font-light px-4">
            Let our experts handle the complexity while you focus on building.
            Get started with a free consultation today.
          </p>
          <div class="flex flex-col sm:flex-row gap-3 sm:gap-4 justify-center px-4"><button
              class="bg-white text-[#1e3a8a] hover:bg-gray-100 px-6 sm:px-8 md:px-12 py-3 md:py-4 rounded-full text-sm sm:text-base md:text-lg font-semibold transition-all duration-300 transform hover:scale-105 shadow-2xl">
              Schedule Consultation
            </button><button
              class="bg-transparent border-2 border-white text-white hover:bg-white hover:text-primary px-6 sm:px-8 md:px-12 py-3 md:py-4 rounded-full text-sm sm:text-base md:text-lg font-semibold transition-all duration-300 transform hover:scale-105">
              View Our Services
            </button></div>
        </div>
      </div>
    </section>
    <footer id="footer" class="bg-[#1e3a8a] text-white pt-16 pb-8">
      <div class="max-w-[1440px] mx-auto px-8">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
          <div><img
              src="https://i0.wp.com/permitsandmore.com/wp-content/uploads/2016/06/cropped-logo-1.png?fit=263%2C60&amp;ssl=1"
              alt="Permits &amp; More Logo" class="h-14 w-auto mb-6">
            <p class="text-white leading-relaxed mb-6">
              Your trusted partner for construction permit processing and
              inspection coordination services throughout Southern California.
            </p>
            <div class="flex space-x-4"><a href="#"
                class="w-10 h-10 bg-white/10 hover:bg-white/20 rounded-full flex items-center justify-center transition-all duration-300"><i
                  class="fa-brands fa-facebook-f"></i></a><a href="#"
                class="w-10 h-10 bg-white/10 hover:bg-white/20 rounded-full flex items-center justify-center transition-all duration-300"><i
                  class="fa-brands fa-twitter"></i></a><a href="#"
                class="w-10 h-10 bg-white/10 hover:bg-white/20 rounded-full flex items-center justify-center transition-all duration-300"><i
                  class="fa-brands fa-linkedin-in"></i></a><a href="#"
                class="w-10 h-10 bg-white/10 hover:bg-white/20 rounded-full flex items-center justify-center transition-all duration-300"><i
                  class="fa-brands fa-instagram"></i></a></div>
          </div>
          <div>
            <h3 class="text-xl font-bold mb-6">Quick Links</h3>
            <ul class="space-y-3">
              <li><a href="#home"
                  class="text-white hover:text-gray-200 transition-colors">Home</a>
              </li>
              <li><a href="#services"
                  class="text-white hover:text-gray-200 transition-colors">Services</a>
              </li>
              <li><a href="#about"
                  class="text-white hover:text-gray-200 transition-colors">About
                  Us</a></li>
              <li><a href="#process"
                  class="text-white hover:text-gray-200 transition-colors">Our
                  Process</a></li>
              <li><a href="#testimonials"
                  class="text-white hover:text-gray-200 transition-colors">Testimonials</a>
              </li>
              <li><a href="#contact"
                  class="text-white hover:text-gray-200 transition-colors">Contact</a>
              </li>
            </ul>
          </div>
          <div>
            <h3 class="text-xl font-bold mb-6">Our Services</h3>
            <ul class="space-y-3">
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Permit
                  Processing</a></li>
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Inspection
                  Coordination</a></li>
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Compliance
                  Support</a></li>
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Commercial
                  Projects</a></li>
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Residential
                  Projects</a></li>
              <li><a href="#"
                  class="text-white hover:text-gray-200 transition-colors">Plan
                  Review</a></li>
            </ul>
          </div>
          <div>
            <h3 class="text-xl font-bold mb-6 text-white">Newsletter</h3>
            <p class="text-white mb-4">Stay updated with the latest industry
              news and permit requirements.</p>
            <form class="space-y-3"><input type="email"
                placeholder="Your email address"
                class="w-full px-4 py-3 rounded-lg bg-gray-300 border border-gray-400 text-gray-900 placeholder-gray-600 focus:border-gray-500 focus:ring-2 focus:ring-gray-400 outline-none transition-all"><button
                type="submit"
                class="w-full bg-[#3b82f6] hover:bg-[#2563eb] text-white py-3 rounded-lg font-semibold transition-all duration-300">
                Subscribe
              </button></form>
          </div>
        </div>
        <div class="border-t border-white/20 pt-8">
          <div class="flex flex-col md:flex-row justify-between items-center">
            <p class="text-white text-sm mb-4 md:mb-0">
              © 2025 Permits &amp; More. All rights reserved.
            </p>
            <div class="flex space-x-6"><a href="#"
                class="text-white hover:text-gray-200 text-sm transition-colors">Privacy
                Policy</a><a href="#"
                class="text-white hover:text-gray-200 text-sm transition-colors">Terms
                of Service</a><a href="#"
                class="text-white hover:text-gray-200 text-sm transition-colors">Sitemap</a>
            </div>
          </div>
        </div>
      </div>
    </footer>
</div>

<style>
  .hero-cta-button {
    transition: background-color 0.3s ease-out 0.05s, transform 0.3s ease-out 0.05s;
  }
  
  .hero-cta-button:hover {
    transition: background-color 0.3s ease-out, transform 0.3s ease-out;
  }
</style>