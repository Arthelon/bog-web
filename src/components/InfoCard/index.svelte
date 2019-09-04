<script>
  import Container from './Container.svelte'

  export let heading = ''
  export let descriptionHTML = ''
  export let img = {
    src: '',
    alt: '',
  }

  export let label = ''
  export let link = ''
  export let linkText = 'Learn more'

  let imgContainer;

  const labels = [
    {
      label: 'In Design',
      color: '#FFEECE',
    },
    {
      label: 'In Development',
      color: '#FFB374',
    },
    {
      label: 'Delivered',
      color: '#FF8988',
    },
  ]

  const lazy = (node, data) => {
    const tempImg = new Image();
    tempImg.setAttribute('src', data.src);
    tempImg.setAttribute('alt', data.alt);
    tempImg.onload = () => {
      tempImg.setAttribute('class', node.getAttribute('class')); // set svelte class
      imgContainer.replaceChild(tempImg, node);
    }
  }
  $: validLabel = labels.find(l => l.label === label)
</script>

<style>
  .img-container {
    height: 27rem;
    width: 100%;
    margin-bottom: 2rem;
    border-radius: inherit;
    background: #333;
    overflow: hidden;
  }
  .img-container > img {
    height: 100%;
    width: auto;
  }
  h3,
  p {
    padding: 0 2rem;
    margin: 1rem 0;
  }
  h3 {
    font-size: var(--small-header-size);
  }
  p {
    margin-bottom: 2rem;
  }
  small {
    font-size: 14px;
    padding: 0.7rem 2rem;
    border-radius: 3rem;
    margin: 3rem 2rem;
    margin-top: auto;
    width: auto;
  }
</style>

<Container {link}>
  <div class="img-container" bind:this={imgContainer}>
    <img use:lazy={img} src={'./example-data/bfa-lazy.jpg'} alt={img.alt} />
  </div>
  <h3>{heading}</h3>
  <p>
    {@html descriptionHTML}
  </p>
  {#if validLabel}
    <small style={`background-color: ${validLabel.color}`}>
      {validLabel.label}
    </small>
  {/if}
</Container>
