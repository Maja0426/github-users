<script>
  import Card from "./components/Card.svelte";
  import MainInfo from "./components/MainInfo.svelte";
  import GitHub from "github-api";
  import moment from "moment";
  let datas = [];
  let githubUser = "";
  let isUser = false;
  let errorMsg = "";

  let user = "";

  function ErrorMsg(message) {
    this.message = message;
    this.name = "ErrorMsg";
  }

  const gh = new GitHub();

  async function handleSubmit() {
    githubUser = gh.getUser(user);
    console.log(githubUser);

    if (githubUser) {
      isUser = true;
      await githubUser.listRepos(function(err, repos) {
        if (!err) {
          console.log(repos);
          datas = repos;
        } else {
          isUser = false;
          throw new ErrorMsg("Something went wrong...");
        }
      });
    }
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  section {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
  }

  img {
    width: 100px;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 300;
  }

  @media (max-width: 420px) {
    section {
      flex-direction: column;
      justify-content: center;
      flex-wrap: nowrap;
    }
  }
</style>

<main>
  <form action="" on:submit|preventDefault={handleSubmit}>
    <input type="text" bind:value={user} />
    <button type="submit">Submit</button>
  </form>
  {#if isUser}
    <h1>{githubUser.__user}</h1>
    <!-- <h3>{githubUser.__user} has {datas.length} repo(s)</h3> -->
    <section>
      <MainInfo reposNumber={datas.length} />
    </section>
    <!-- <img src={user} alt="{githubUser.__user} avatar" /> -->
    <section>
      {#each datas as data}
        <Card
          repoName={data.name}
          repoDescription={data.description !== null ? data.description : ''}
          repoUrl={data.html_url}
          repoLanguage={data.language}
          repoSize={data.size}
          repoCreatedAt={moment(data.created_at).format('llll')} />
      {/each}
    </section>
  {:else}
    <h2>No Github User!!</h2>
  {/if}
</main>
