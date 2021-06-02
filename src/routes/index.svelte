<script>
  import SearchBox from "$lib/SearchBox/index.svelte";
  import Facet from "$lib/Facet/index.svelte";
  import ResultList from "$lib/ResultList/index.svelte";
  import { Col, Container, Row } from 'sveltestrap';
</script>

<svelte:head>
  <title>Coveo Headless + Svelte</title>
</svelte:head>

<Row>
  <Col xs="3">
    <Facet title="Object type" field="objecttype"/>
    <Facet title="Author" field="author"/>
  </Col>
  <Col>
    <SearchBox searchAsYouTypeDelay={0}/>
    <ResultList />
  </Col>
</Row>