<script>
  import { getContext } from "svelte"
  import { CldOgImage, CldImage } from "svelte-cloudinary"

  export let data

  const posts = getContext("posts")
  const post = posts.find(p => p.slug === `/blog/${data.slug}`)

  function wrapText(text) {
    return text.match(/.{1,10}/g).join("\n")
  }
</script>

<CldOgImage src={post.image_id} />

<main>
  <a class="home-link" href="/">&lt; Go Home</a>
  <div class="heading-with-dash">
    <h1>{post.title}</h1>
  </div>
  <div class="post__cover">
    <!-- <CldImage
      width={960}
      height={600}
      src={post.image_id}
      alt={post.image_alt}
    /> -->
    <CldImage
      width={960}
      height={600}
      src={post.image_id}
      alt={post.image_alt}
      blur="500"
      overlays={[
        {
          text: {
            color: "white",
            fontFamily: "Poppins",
            fontSize: "80",
            fontWeight: "bold",
            lineSpacing: "14",
            text: wrapText(post.title),
            // text: post.title,
          },
        },
      ]}
    />
  </div>
  <div class="post__content">{@html post.html}</div>
</main>

<style>
  .home-link {
    color: #aaa;

    &:hover {
      color: yellow;
    }
  }

  h1 {
    color: white;
    font-size: 3rem;
  }

  .post__cover {
    border-radius: 5px;
    overflow: hidden;
    margin: 20px 0;
  }

  .post__content {
    color: white;
    max-width: 700px;
    margin: 0 auto;
    padding: 20px 0;
  }

  .post__content :global(h2) {
    margin: 20px 0;
    font-size: 2rem;
    color: yellow;
  }

  .post__content :global(p) {
    margin: 0 0 30px;
    font-size: 1.2rem;
    line-height: 1.7;
  }

  .post__content :global(img) {
    margin-bottom: 30px;
    border-radius: 10px;
  }
</style>
