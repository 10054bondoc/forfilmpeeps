<script>
import { fade } from 'svelte/transition';
$: navbar_width = '4%';
$: paper_clip = false;

const navbar_items = [
  { text: 'Projects', icon: 'film-outline' },
  { text: 'Community', icon: 'people-outline' },
];

const open_navbar = (e) => {
  if (!paper_clip) {
    e.target.style.width = '15%';
    navbar_width = '15%';
  }
};

const close_navbar = (e) => {
  if (!paper_clip) {
    navbar_width = '4%';
    e.target.style.width = navbar_width;
  }
};

const trigger_paperclip = () => {
  paper_clip = !paper_clip;
};
</script>

<main>
  <div class="header">
    <img src="beelogo.png" alt="beelogo" />
    <span style="font-size: 2.5rem; font-weight: 800;">FILMER</span>
  </div>
  <div
    class="navbar"
    style="width:{paper_clip ? '15%' : '4%'};"
    on:mouseenter="{open_navbar}"
    on:mouseleave="{close_navbar}"
  >
    <div class="navbar_headspace">
      {#if navbar_width !== '4%'}
        <ion-icon
          id="paperclip"
          name="attach-outline"
          on:click="{trigger_paperclip}"
          style="opacity: {paper_clip ? '1' : '.3'}"></ion-icon>
      {/if}
    </div>
    <div class="navbar-contents">
      {#each navbar_items as item}
        <div style="{'margin-bottom: 2rem;'}">
          <ion-icon
            name="{item.icon}"
            style="{'min-width: 1em; min-height: 1em;'}"></ion-icon>
          {#if navbar_width !== '4%'}
            <p transition:fade>{item.text}</p>
          {/if}
        </div>
      {/each}
    </div>
  </div>
</main>

<style>
main {
  background-color: var(--mainbg);
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.header {
  width: 100%;
  height: 5rem;
  background-color: var(--lightest2);

  padding: 1rem;

  color: var(--mainbg);
  font-size: 2.25rem;
  font-weight: 800;

  display: flex;
  align-items: center;
}

.navbar {
  height: 100%;
  background-color: var(--darkest1);

  justify-content: center;
  padding: 1rem;

  transition: 0.5s;

  position: relative;
}

img {
  width: 3.5rem;
  height: 3.5rem;
  margin-right: 1rem;
  left: 5rem;
}
.navbar_headspace {
  display: flex;
  justify-content: flex-end;
  position: absolute;
  right: 0;
  top: 0.5rem;

  color: var(--lightest1);
  font-size: 2rem;
}
.navbar-contents {
  margin-top: 4rem;
  display: flex;

  flex-direction: column;
  transition: 1s;
}

.navbar-contents > * {
  color: var(--lightest1);
  opacity: 0.6;
  font-size: 3rem;
  cursor: pointer;

  display: flex;
  align-items: center;
}
.navbar-contents > *:hover {
  opacity: 0.9;
}

p {
  font-size: 1.7rem;
  font-weight: 400;
  margin-left: 1.9rem;
}

#paperclip {
  cursor: pointer;
}
</style>
