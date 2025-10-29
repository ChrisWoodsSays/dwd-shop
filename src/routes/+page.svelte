<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';
  let featuredItems = [];

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    gsap.from('.hero-title, .hero-nav a', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

    gsap.utils.toArray('.project').forEach((proj) => {
      gsap.from(proj.querySelector('.project-image img'), {
        scale: 1.03,
        duration: 1.1,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: proj,
          start: 'top 90%',
          toggleActions: 'play none none none'
        }
      });
      gsap.from(proj.querySelector('.project-content'), {
        opacity: 0,
        y: 36,
        duration: 0.9,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: proj,
          start: 'top 85%',
          toggleActions: 'play none none none'
        }
      });
    });


    // Example featured items array
    featuredItems = [
      {
        image: '/images/featured1.jpg',
        title: 'Gospel Journey Planner',
        description: 'Plan your journey through the Bible with clarity and ease.',
        link: 'https://www.etsy.com/uk/listing/xxxx'
      },
      {
        image: '/images/featured2.jpg',
        title: 'Data Visualization Print',
        description: 'Beautifully designed print for data enthusiasts.',
        link: 'https://www.etsy.com/uk/listing/yyyy'
      },
      {
        image: '/images/featured3.jpg',
        title: 'Interactive Dashboard',
        description: 'Engage with your data interactively online.',
        link: 'https://www.etsy.com/uk/listing/zzzz'
      }
    ];


  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');

  :global(body) {
    margin: 0;
    font-family: 'Comfortaa', cursive;
    background: #fff;
    color: #222;
  }

  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2.5rem 1.75rem;
  }

  /* ===== HERO ===== */
  .hero-top {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 1.5rem;
    position: relative; /* for profile image */
  }

  .hero-left {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .hero-title {
    font-size: 2.2rem;
    color: #4169e1;
    margin: 0;
  }

  .hero-nav {
    display: flex;
    gap: 1.25rem;
    flex-wrap: wrap;
    font-weight: 600;
  }

  .hero-nav a {
    color: #4169e1;
    text-decoration: none;
    font-size: 0.98rem;
  }
  .hero-nav a:hover {
    color: #2746b3;
  }

  /* profile image: always top right */
  .hero-profile {
    width: 84px;
    height: 84px;
    border-radius: 50%;
    object-fit: cover;
    position: absolute;
    top: 0;
    right: 0;
  }

  .hero-intro {
    margin-bottom: 3rem;
    max-width: 76ch;
    color: #333;
    line-height: 1.48;
    font-size: 1.05rem;
  }

    .featured-grid {
    display: flex;
    gap: 2rem;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  .featured-item {
    flex: 1 1 calc(33.333% - 1.33rem); /* 3 items per row with gaps */
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    margin-bottom: 2rem;
  }

  .featured-item img {
    width: 100%;
    max-width: 300px;
    height: auto;
    border-radius: 4px;
    box-shadow: 0 6px 18px rgba(0,0,0,0.05);
    margin-bottom: 0.75rem;
  }

  .featured-item h3 {
    margin: 0.5rem 0 0.25rem 0;
    font-size: 1.25rem;
    color: #222;
  }

  .featured-item p {
    font-size: 0.95rem;
    color: #333;
    margin-bottom: 0.5rem;
  }

  .featured-item a.button {
    padding: 0.5rem 0.9rem;
    background: #4169e1;
    color: #fff;
    text-decoration: none;
    border-radius: 4px;
    font-weight: 600;
  }

  .featured-item a.button:hover {
    background: #2746b3;
  }

  /* Responsive: stack items vertically on narrow screens */
  @media (max-width: 900px) {
    .featured-item {
      flex: 1 1 100%;
    }
  }

  /* ===== PROJECTS ===== */
  .project {
    display: flex;
    gap: 3rem;
    margin-bottom: 3rem;
    border-bottom: 1px solid rgba(0,0,0,0.08);
    padding-bottom: 2rem;
    align-items: flex-start;
  }

  .project.left-image {
    flex-direction: row;
  }

  .project.right-image {
    flex-direction: row-reverse;
  }

  .project-image {
    flex: 1 1 45%;
    min-width: 250px;
    min-height: 320px;
    overflow: hidden;
    border: 1px solid rgba(0,0,0,0.08);
    box-shadow: 0 8px 22px rgba(0,0,0,0.06);
    border-radius: 4px;
  }

  .project-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 4px;
    display: block;
  }

  .project-content {
    flex: 1 1 45%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .project-content h2 {
    margin: 0 0 0.75rem 0;
    font-size: 1.6rem;
    color: #222;
  }

  .project-content p {
    margin: 0 0 0.5rem 0;
    color: #333;
    line-height: 1.45;
    font-size: 1rem;
  }

  .project-content a.button {
    display: inline-block;
    padding: 0.5rem 0.9rem;
    background: #4169e1;
    color: #fff;
    text-decoration: none;
    border-radius: 4px;
    align-self: flex-start;
    font-weight: 600;
  }
  .project-content a.button:hover {
    background: #2746b3;
  }

  /* ===== SERVICES ===== */
  #services {
    margin-top: 4rem;
    padding-top: 2rem;
    border-top: 1px solid rgba(0,0,0,0.08);
  }

  footer {
    margin-top: 4rem;
    color: #777;
    font-size: 0.95rem;
  }

  /* ===== RESPONSIVE ===== */
  @media (max-width: 980px) {
    .project {
      flex-direction: column !important;
    }
    .project-image, .project-content {
      flex: 1 1 100%;
    }
    .project-image { min-height: 220px; }
  }

  @media (max-width: 520px) {
    .hero-title { font-size: 1.6rem; }
    .hero-intro { font-size: 1rem; }
    .hero-profile { width: 68px; height: 68px; }
  }
</style>

<main>
  <!-- HERO -->
  <div class="hero-top">
    <div class="hero-left">
      <h1 class="hero-title">Drawing with Data</h1>
      <nav class="hero-nav" aria-label="top nav">
        <a href="https://www.etsy.com/uk/listing/xxxx" target="_blank" rel="noopener">Buy Gospel Journey Planner</a>
        <a href="#projects">Portfolio</a>
        <a href="#services">My Services</a>
      </nav>
    </div>

    <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" class="hero-profile" />
  </div>

  <!-- INTRO PARAGRAPH -->
  <p class="hero-intro">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

  <!-- FEATURED SECTION -->
<section id="featured" style="margin-bottom: 3rem;">
  <div class="featured-grid">
    {#each featuredItems as item}
      <div class="featured-item">
        <img src={item.image} alt={item.title} />
        <h3>{item.title}</h3>
        <p>{item.description}</p>
        {#if item.link}
          <a class="button" href={item.link} target="_blank" rel="noopener">Buy</a>
        {/if}
      </div>
    {/each}
  </div>
</section>

  <!-- PROJECTS -->
  <section id="projects" aria-label="portfolio">
    {#each projects as project, i}
      <article class="project {i % 2 === 0 ? 'left-image' : 'right-image'}">
        <div class="project-image" aria-hidden="true">
          <img src={project.image} alt={project.title} />
        </div>
        <div class="project-content">
          <div><h2>{project.title}</h2></div>
          <div>
            <p>{project.description}</p>
            {#if project.link}
              <a class="button" href={project.link} target="_blank" rel="noopener">
                {project.featured ? 'Buy Print' : 'View Project'}
              </a>
            {/if}
          </div>
        </div>
      </article>
    {/each}
  </section>

  <!-- SERVICES -->
  <section id="services">
    <h2>My Services</h2>
    <p>Describe your services here. This section is linked from the top nav.</p>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>
