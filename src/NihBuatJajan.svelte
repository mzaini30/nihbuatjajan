<script>
  import { acak } from "kumpulan-tools";
  const { username } = $props();
  let donasi = [];
  let tampil = $state("");
  let triggerTampil = $state(false);
  async function dapatkan() {
    let halaman = await fetch(
      `https://cors.mabaiz.web.id/?link=https://www.nihbuatjajan.com/${username}`,
    );
    halaman = await halaman.text();
    let domHalaman = new DOMParser().parseFromString(halaman, "text/html");
    let donation = domHalaman.querySelectorAll(".donation");
    if (donation.length > 0) {
      for (let x of donation) {
        donasi = [...donasi, x.querySelector(".donator").innerHTML.trim()];
      }
      tampil = donasi[0];
      triggerTampil = true;
    }
  }
  dapatkan();
</script>

{#if triggerTampil}
  <div class="alert alert-success flex justify-between" role="alert">
    <div>
      {@html tampil}
    </div>
    <button
      onclick={() => (triggerTampil = false)}
      type="button"
      class="btn-close"
      data-bs-dismiss="alert"
      aria-label="Close"
    ></button>
  </div>
{/if}
<a
  href="https://www.nihbuatjajan.com/{username}"
  class="fixed bottom-2 right-2 btn btn-primary"
  target="_blank">Support</a
>
