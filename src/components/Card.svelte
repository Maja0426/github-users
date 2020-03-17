<script>
  export let repoName;
  export let repoDescription;
  export let repoUrl;
  export let repoSize;
  export let repoLanguage;
  export let repoCreatedAt;
</script>

<style>
  .card {
    padding: 1em;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 28%;
    margin: 1em;
    border: 1px solid rgb(223, 221, 221);
    box-shadow: 2px 2px 8px rgb(223, 221, 221);
  }

  .card-footer p {
    justify-content: flex-start;
  }

  @media (max-width: 420px) {
    .card {
      width: calc(100% - 2em);
      margin: 1em 0;
    }
  }
</style>

<div class="card">
  <div class="card-header">
    <h3>{repoName}</h3>
  </div>
  <div class="card-body">
    <p>{repoDescription}</p>
    <p>
      <a href={repoUrl} target="_blank" rel="noreferrer">{repoUrl}</a>
    </p>
  </div>
  <div class="card-footer">
    <p>{repoLanguage} | {repoSize} KB</p>
    <p>Created: {repoCreatedAt}</p>
  </div>
</div>
