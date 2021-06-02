<script>
  import { Styles } from 'sveltestrap';
  import { Col, Container, Row } from 'sveltestrap';
</script>

<Styles />

<svelte:head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootswatch@4.5.2/dist/superhero/bootstrap.min.css">
</svelte:head>

<header>
  My Header here
</header>

<main>
  <Container fluid>
    <slot />
  </Container>
</main>

<footer>
	My footer here
</footer>

<style>
  header,footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 40px;
  }
  @media (min-width: 480px) {
    footer {
      padding: 40px 0;
    }
  }
</style>