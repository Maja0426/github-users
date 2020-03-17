<script>
  export let reposNumber;
</script>

<style>
  .info-box {
    display: flex;
    flex-direction: column;
    margin: 1em;
    justify-content: center;
    align-items: center;
    min-width: 200px;
    background: #222;
    color: #fff;
  }

  @media (max-width: 420px) {
    .info-box {
      width: 100%;
      margin: 1em 0;
    }
  }
</style>

<div class="info-box">
  <h3>{reposNumber}</h3>
  <p>Public repositories</p>
</div>
