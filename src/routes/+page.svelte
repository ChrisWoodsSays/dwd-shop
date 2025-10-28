<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    // Intro animation
    gsap.from('.hero-top, .hero-intro', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

    // Animate projects on scroll
    gsap.utils.toArray('.project').forEach((proj) => {
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
    });
  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');

  :global(body) {
    margin: 0;
    font-family: 'Comfortaa', cursive;
    background: #fff;
    color: #222;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  /* ===== Layout ===== */
  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2.5rem 2rem;
  }

  :root {
    --gutter: 3rem;       /* space between image and text */
    --outer-pad: 2rem;    /* margin from outer edge */
  }

  /* ===== Header ===== */
  .hero-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .title {
    font-size: 2.1rem;
    color: #4169e1;
    margin: 0;
  }

  .hero-nav {
    display: flex;
    gap: 1.25rem;
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

  .hero-profile {
    width: 84px;
    height: 84px;
    border-radius: 50%;
    object-fit: cover;
    flex-shrink: 0;
  }

  /* ===== Intro paragraph ===== */
  .hero-intro {
    margin: 0 0 2.25rem 0;
    max-width: 76ch;
    color: #333;
    line-height: 1.48;
    font-size: 1.05rem;
  }

  /* ===== Projects grid ===== */
  #projects {
    margin: 0;
  }

  .project {
    display: grid;
    grid-template-columns: 1fr var(--gutter) 1fr;
    align-items: stretch;
    margin-bottom: 3.5rem;
  }

  /* Fix for narrow browser widths */
  .project-image,
  .project-content {
    min-width: 0;
  }

  /* Left-image layout */
  .project.left-image .project-image {
    grid-column: 1;
    justify-self: stretch;
  }
  .project.left-image .project-content {
    grid-column: 3;
    justify-self: stretch;
    padding-left: var(--gutter); /* text perfectly aligns with image edge */
    padding-right: 0;
  }

  /* Right-image layout */
  .project.right-image .project-image {
    grid-column: 3;
    justify-self: stretch;
  }
  .project.right-image .project-content {
    grid-column: 1;
    justify-self: stretch;
    padding-right: var(--gutter);
    padding-left: 0;
  }

  /* ===== Image styling ===== */
  .project-image {
    width: 100%;
    height: 100%;
    min-height: 320px;
    overflow: hidden;
    border-radius: 6px;
    border: 1px solid rgba(0,0,0,0.08);
    box-shadow: 0 6px 18px rgba(0,0,0,0.07);
  }

  .project-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  /* ===== Content styling ===== */
  .project-content {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
  }

  .project-content h2 {
    margin: 0 0 0.75rem 0;
    font-size: 1.6rem;
    color: #222;
  }

  .project-content p {
    margin: 0;
    color: #333;
    line-height: 1.45;
    font-size: 1rem;
  }

  /* ===== Buttons ===== */
  .bottom-content {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .project-content a.button {
    display: inline-block;
    padding: 0.5rem 0.9rem;
    background: #4169e1;
    color: #fff;
    text-decoration: none;
    border-radius: 6px;
    font-weight: 600;
    align-self: flex-start;
  }

  .project-content a.button:hover {
    background: #2746b3;
  }

  /* ===== Services Section ===== */
  #services {
    margin-top: 4rem;
    border-top: 1px solid rgba(0,0,0,0.08);
    padding-top: 3rem;
  }

  #services h2 {
    font-size: 1.8rem;
    margin-bottom: 1rem;
    color: #222;
  }

  #services p {
    max-width: 70ch;
    color: #333;
    line-height: 1.5;
  }

  /* ===== Footer ===== */
  footer {
    margin-top: 3rem;
    color: #777;
    font-size: 0.95rem;
  }

  /* ===== Responsive ===== */
  @media (max-width: 980px) {
    main {
      padding: 2rem 1.25rem;
    }
    :root {
      --gutter: 1.25rem;
      --outer-pad: 1.25rem;
    }
    .project {
      grid-template-columns: 1fr;
    }
    .project-image {
      min-height: 220px;
    }
    .project.left-image .project-content,
    .project.right-image .project-content {
      padding: 1rem 0 0 0;
    }
  }

  @media (max-width: 520px) {
    .title {
      font-size: 1.6rem;
    }
    .hero-intro {
      font-size: 1rem;
    }
    .hero-profile {
      width: 68px;
      height: 68px;
    }
  }
</style>

<main>
  <!-- ===== HEADER ===== -->
  <div class="hero-top">
    <div class="hero-left">
      <h1 class="title">Drawing with Data</h1>
    </div>

    <div style="display:flex; align-items:center; gap:1rem;">
      <nav class="hero-nav" aria-label="top nav">
        <a href="https://www.etsy.com/uk/listing/xxxx" target="_blank" rel="noopener">Buy Gospel Journey Planner</a>
        <a href="#projects">Portfolio</a>
        <a href="#services">My Services</a>
      </nav>

      <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" class="hero-profile" />
    </div>
  </div>

  <!-- ===== INTRO ===== -->
  <p class="hero-intro">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

  <!-- ===== PROJECTS ===== -->
  <section id="projects" aria-label="portfolio">
    {#each projects as project, i}
      <article class="project {i % 2 === 0 ? 'left-image' : 'right-image'}" role="article" aria-labelledby={"p"+i}>
        <div class="project-image" aria-hidden="true">
          <img src={project.image} alt={project.title} />
        </div>

        <div class="project-content" id={"p"+i}>
          <div>
            <h2>{project.title}</h2>
          </div>

          <div class="bottom-content">
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

  <!-- ===== SERVICES SECTION ===== -->
  <section id="services" aria-label="services">
    <h2>My Services</h2>
    <p>
      I create bespoke data visualisations and interactive graphics to help organisations tell their stories clearly.
      My work includes custom web dashboards, printed infographics, exploratory data tools, and maps. Whether your goal
      is communication, insight, or engagement, I combine analysis, design, and narrative to produce visuals that work.
    </p>
  </section>

  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>
