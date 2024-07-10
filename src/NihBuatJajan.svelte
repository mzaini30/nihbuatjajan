<script>
  const { username } = $props();
  async function dapatkan() {
    let halaman = await fetch(
      `https://cors.mabaiz.web.id/?link=https://www.nihbuatjajan.com/${username}`,
    );
    halaman = await halaman.text();
    let domHalaman = new DOMParser().parseFromString(halaman, "text/html");
    console.log(domHalaman);
  }
  dapatkan();
</script>
