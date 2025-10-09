<script>
  const profile = {
    name: "Chris Woods",
    strapline: "Information Designer & Artist",
    image: "images/Profile Nov 24 Square.jpg",
    links: [
      { name: "Instagram", url: "https://instagram.com/drawingwithdata" },
      { name: "Etsy", url: "https://etsy.com/shop/drawingwithdata" },
      { name: "Website", url: "https://www.drawingwithdata.com" }
    ]
  };

  // Example poster items — replace src with your images and update descriptions
  const posters = [
    { src: '/images/JP1.jpeg', alt: 'Poster 1', description: 'A gospel journey print — overview of core themes.' },
    { src: '/images/JP2.jpeg', alt: 'Poster 2', description: 'Chronological map with visual landmarks.' },
    { src: '/images/JP3.jpeg', alt: 'Poster 3', description: 'Key characters and relationships illustrated.' },
  ];
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
    <h2 class="gallery-title">The Gospel Journey Planner</h2>
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
  :global(html, body) {
    height: 100%;
    margin: 0;
    font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  main {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    background: linear-gradient(to bottom, #0077ff 0%, white 100%); /* flipped gradient */
    color: white;
  }

  .hero {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 3rem 1rem;
    text-align: center;
  }

  .profile {
    max-width: 780px;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .profile-image {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    object-fit: cover;
    border: 4px solid rgba(255,255,255,0.9);
    box-shadow: 0 10px 30px rgba(0,0,0,0.25);
    margin-bottom: 1.25rem;
    background: #eee;
  }

  h1 {
    font-size: 2rem;
    margin: 0.25rem 0;
    line-height: 1.1;
    text-shadow: 0 2px 6px rgba(0,0,0,0.25);
  }

  .strapline {
    font-size: 1.05rem;
    font-weight: 300;
    margin: 0.5rem 0 1.5rem 0;
    max-width: 90%;
    text-shadow: 0 1px 4px rgba(0,0,0,0.22);
  }

  .buttons {
    display: flex;
    gap: 0.8rem;
    flex-direction: column;
    width: 100%;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
  }

  .button {
    background: rgba(255,255,255,0.15);
    color: white;
    text-decoration: none;
    padding: 0.75rem 1rem;
    border-radius: 8px;
    font-weight: 600;
    transition: background 0.18s ease, transform 0.15s ease;
    min-width: 160px;
    text-align: center;
  }

  .button:hover { transform: translateY(-3px); background: rgba(255,255,255,0.25); }

  .gallery {
    background: transparent;
    color: #0b1b2b;
    padding: 3rem 1rem 6rem 1rem;
  }

  .gallery-title {
    color: #0b1b2b; /* dark color for contrast */
    text-align: center;
    margin: 0 0 1.5rem 0;
    font-size: 1.5rem;
    text-shadow: none;
  }

  .grid {
    display: grid;
    gap: 1.5rem;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    align-items: start;
    max-width: 1100px;
    margin: 0 auto;
  }

  .poster {
    background: white;
    border-radius: 6px;
    padding: 0.5rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    box-shadow: 0 18px 30px rgba(6,18,50,0.25), 0 6px 12px rgba(6,18,50,0.14); /* slightly stronger shadows */
    transform-origin: center;
    transition: transform 0.18s ease, box-shadow 0.18s ease;
  }

  .poster img {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 4px;
    object-fit: cover;
  }

  .poster figcaption {
    margin-top: 0.65rem;
    font-size: 0.95rem;
    color: #0b1b2b;
    text-align: center;
    padding: 0 0.25rem 0.6rem 0.25rem;
  }

  .poster:hover {
    transform: translateY(-8px) rotate(-0.25deg);
    box-shadow: 0 30px 50px rgba(6,18,50,0.28), 0 10px 18px rgba(6,18,50,0.16); /* slightly stronger hover shadows */
  }

  @media (max-width: 480px) {
    .gallery { padding-bottom: 4rem; }
    .buttons { width: 100%; }
    .button { width: 100%; max-width: none; }
  }

  @media (min-width: 600px) {
    h1 { font-size: 2.5rem; }
    .strapline { font-size: 1.15rem; }
    .buttons { flex-direction: row; }
    .button { min-width: 140px; }
  }

  @media (min-width: 1200px) {
    .hero { padding-top: 4.5rem; padding-bottom: 4.5rem; }
    .gallery { padding-top: 4rem; }
  }
</style>
