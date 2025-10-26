<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
  // Hero animation
  const tl = gsap.timeline({ defaults: { ease: 'power2.out', duration: 1 } });
  tl.from('header img', { opacity: 0, y: 40 })
    .from('header h1', { opacity: 0, y: 20 }, '-=0.6')
    .from('header p', { opacity: 0, y: 20, stagger: 0.15 }, '-=0.4');

  // Scroll-triggered section animations
  const sections = gsap.utils.toArray('section');
  sections.forEach((section) => {
    const img = section.querySelector('img');
    const content = section.querySelector('.content');

    // Animate the section wrapper itself
    gsap.fromTo(
      section,
      { opacity: 0, y: 50 },
      {
        opacity: 1,
        y: 0,
        duration: 1,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: section,
          start: 'top 85%',
          toggleActions: 'play none none none',
        },
      }
    );

    // Optional: stagger image and content slightly for nice effect
    gsap.fromTo(
      [img, content],
      { opacity: 0, y: 20 },
      {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: 'power2.out',
        stagger: 0.15,
        scrollTrigger: {
          trigger: section,
          start: 'top 85%',
          toggleActions: 'play none none none',
        },
      }
    );
  });
});



</script>

<main>
  <header class="hero">
    <div class="profile">
      <img src={profile.image} alt="Chris Woods" class="profile-image" />
      <h1>{profile.name}</h1>
      <p class="strapline">{profile.strapline}</p>
      <div class="buttons">
        {#each profile.links as link}
          <a href={link.url} target="_blank" rel="noopener noreferrer" class="button">{link.name}</a>
        {/each}
      </div>
    </div>
  </header>

  <section class="gallery" aria-label="Poster gallery">
    <h2 class="gallery-title">The Gospel Journey Planner (c) 2025 Chris Woods</h2>
    <div class="grid">
      {#each posters as p}
        <figure class="poster">
          <img src={p.src} alt={p.alt} loading="lazy" />
          <figcaption>{p.description}</figcaption>
        </figure>
      {/each}
    </div>
  </section>
</main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');

  main {
    font-family: 'Comfortaa', cursive;
    color: #222;
    background: #fff;
  }

  header {
    text-align: center;
    padding: 4rem 1rem 3rem;
    overflow: hidden;
  }

  header img {
    width: 160px;
    height: 160px;
    border-radius: 50%;
    object-fit: cover;
    margin-bottom: 1rem;
    border: 4px solid #4169e1;
  }

  header h1 {
    color: #4169e1;
    font-size: 2.7rem;
    margin-bottom: 0.5rem;
  }

  header p {
    max-width: 600px;
    margin: 0.6rem auto;
    font-size: 1.1rem;
    line-height: 1.5;
  }

  header a {
    color: #4169e1;
    text-decoration: none;
    font-weight: bold;
  }

  section {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 3rem 0;
    opacity: 0; /* hidden until GSAP fades in */
  }

  section img {
    width: 100%;
    max-height: 80vh;
    object-fit: cover;
    border-radius: 0.5rem;
  }

  .content {
    padding: 1.5rem;
    max-width: 900px;
  }

  .content h2 {
    color: #4169e1;
    margin-bottom: 0.5rem;
  }

  .content p {
    line-height: 1.5;
    margin-bottom: 1rem;
  }

  .button {
    display: inline-block;
    background: #4169e1;
    color: white;
    text-decoration: none;
    padding: 0.75rem 1.25rem;
    border-radius: 999px;
    transition: 0.2s;
  }

  .button:hover {
    background: #2746b3;
  }

  footer {
    text-align: center;
    padding: 2rem;
    font-size: 0.9rem;
    color: #777;
  }

  footer a {
    color: #4169e1;
    text-decoration: none;
  }

  @media (min-width: 768px) {
    section {
      flex-direction: row;
      align-items: stretch;
    }

    section:nth-child(even) {
      flex-direction: row-reverse;
    }

    section img {
      width: 50%;
    }

    .content {
      width: 50%;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
  }

  /* Featured Etsy print styling */
  section.featured {
    background: #f4f8ff;
    border-top: 4px solid #4169e1;
    border-bottom: 4px solid #4169e1;
    padding: 2rem 0;
  }
</style>

<main>
  <header>
    <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" />
    <h1>Drawing with Data</h1>
    <p>
      Data, insight and design, mixed with technology, enable us to see what’s
      going on in the world, tell stories that matter, and make a difference.
    </p>
    <p>
      I can help bring your data to life through static or interactive
      visualisation — with a focus on Christian organisations, active travel,
      cycling, environment and social justice.
    </p>
    <p>
      <a href="https://www.linkedin.com/in/chriswooods" target="_blank"
        >Connect on LinkedIn</a
      >
    </p>
  </header>

  {#each projects as project}
    <section class:featured={project.featured}>
      <img src={project.image} alt={project.title} />
      <div class="content">
        <h2>{project.title}</h2>
        <p>{project.description}</p>
        {#if project.link}
          <a class="button" href={project.link} target="_blank">
            {project.featured ? 'Visit Shop' : 'View Project'}
          </a>
        {/if}
      </div>
    </section>
  {/each}

  <footer>
    <p>© Chris Woods 2016–25 | <a href="https://html5up.net">HTML5 UP</a></p>
  </footer>
</main>
