<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    gsap.from('.hero-top, .hero-intro', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

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
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background: #fff;
    color: #222;
  }

  /* page container */
  main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2.5rem 1.75rem;
  }

  /* hero top row */
  .hero-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    margin-bottom: 1.25rem;
    flex-wrap: wrap;
  }
  .title { font-size: 2.15rem; color: #4169e1; margin: 0; line-height: 1; }
  .hero-left { display:flex; align-items:center; gap:1rem; }
  .hero-nav { display:flex; gap:1.25rem; font-weight:600; white-space:nowrap; }
  .hero-nav a { color:#4169e1; text-decoration:none; font-size:0.98rem; }
  .hero-nav a:hover{ color:#2746b3; }
  .hero-profile { width:84px; height:84px; border-radius:50%; object-fit:cover; flex-shrink:0; }

  .hero-intro {
    margin: 0 0 2rem 0;
    max-width: 76ch;
    color: #333;
    line-height: 1.48;
    font-size: 1.05rem;
  }

  /* GRID system for projects:
     left column | gutter | right column
     columns are fixed so inner edges (next to gutter) align perfectly */
  :root {
    --gutter: 3rem;         /* central gutter size */
  }

  #projects { margin: 0; }

  .project {
    display: grid;
    grid-template-columns: 1fr var(--gutter) 1fr;
    gap: 0;
    align-items: stretch;
    margin-bottom: 3.25rem;
  }

  /* for left-image: image in column 1, content in column 3 */
  .project.left-image .project-image { grid-column: 1; }
  .project.left-image .project-content { grid-column: 3; }

  /* for right-image: image in column 3, content in column 1 */
  .project.right-image .project-image { grid-column: 3; }
  .project.right-image .project-content { grid-column: 1; }

  /* image column styling */
  .project-image {
    width: 100%;
    height: 100%;
    min-height: 320px;            /* consistent visual height */
    overflow: hidden;
    border: 1px solid rgba(0,0,0,0.08);
    box-shadow: 0 8px 22px rgba(0,0,0,0.06);
  }
  .project-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    border-radius: 0;              /* square corners */
  }

/* content column */
.project-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 1.75rem 0; /* vertical spacing only */
}


/* alignments — adjust padding to match inner edges perfectly */
.project.left-image .project-content {
  padding-left: 1.5rem;   /* keeps left text slightly off the outer edge */
  padding-right: 0;       /* ensures inner edge lines up with right image */
}

.project.right-image .project-content {
  padding-right: 0;       /* remove extra indent so text aligns with right image */
  padding-left: 1.5rem;   /* keeps left edge (gutter side) consistent */
}

  .project-content h2 { margin: 0 0 .75rem 0; font-size: 1.6rem; color:#222; }
  .project-content p { margin: 0; color: #333; line-height:1.45; font-size:1rem; }

  .bottom-content { display:flex; flex-direction:column; gap:.75rem; }
  .project-content a.button {
    display:inline-block;
    padding: .5rem .9rem;
    background:#4169e1;
    color:#fff;
    text-decoration:none;
    border-radius:0; /* square */
    align-self:flex-start;
    font-weight:600;
  }
  .project-content a.button:hover{ background:#2746b3; }

  /* small helper to ensure top title aligns visually with images top:
     give the title container a small top padding so it never touches the top edge */
  .project-content > div:first-child { padding-top: 0.25rem; }

  /* footer */
  footer { margin-top: 3rem; color:#777; font-size:0.95rem; }

  /* RESPONSIVE: stack into a single column and keep consistent insets */
  @media (max-width: 980px) {
    main { padding: 2rem 1.25rem; }
    :root { --gutter: 1.25rem; }
    .project { grid-template-columns: 1fr; }
    .project-image { min-height: 220px; }
    .project.left-image .project-image,
    .project.right-image .project-image { grid-column: 1; }
    .project.left-image .project-content,
    .project.right-image .project-content { grid-column: 1; padding: 1rem 0; }
    .project-content { padding-left: 0; padding-right: 0; }
  }

  @media (max-width: 520px) {
    .title { font-size: 1.6rem; }
    .hero-intro { font-size: 1rem; }
    .hero-profile { width:68px; height:68px; }
  }
</style>

<main>
  <!-- top row -->
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

  <!-- intro paragraph -->
  <p class="hero-intro">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

  <!-- projects: grid ensures inner edges align -->
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

  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>
