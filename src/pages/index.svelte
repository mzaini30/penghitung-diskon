<script>
  let tab = "menghitung diskon"; // menghitung diskon & membuat diskon
  // $: console.log(tab);

  let harga_sebelumnya;
  let diskon;
  let harga_setelahnya;
  let besarnya_diskon;

  function hitung_diskon() {
    if (!isNaN(harga_sebelumnya) && !isNaN(diskon)) {
      if (tab == "menghitung diskon") {
        harga_setelahnya = ((100 - diskon) / 100) * harga_sebelumnya;
      } else if (tab == "membuat diskon") {
        harga_setelahnya = ((100 + +diskon) / 100) * harga_sebelumnya;
      }
      besarnya_diskon = Math.abs(harga_sebelumnya - harga_setelahnya);
      besarnya_diskon = (~~besarnya_diskon).toLocaleString();
      harga_setelahnya = (~~harga_setelahnya).toLocaleString();
    }
  }
  $: tab ? hitung_diskon() : hitung_diskon();
  $: harga_sebelumnya ? hitung_diskon() : hitung_diskon();
  $: diskon ? hitung_diskon() : hitung_diskon();
</script>

<div class="grid grid-cols-2 menu border-b shadow">
  <label class={tab == "menghitung diskon" ? "bg-gray-200" : null}>
    <input
      type="radio"
      value="menghitung diskon"
      bind:group={tab}
      name=""
      id=""
    /> menghitung diskon
  </label>
  <label class={tab == "membuat diskon" ? "bg-gray-200" : null}>
    <input type="radio" name="" id="" value="membuat diskon" bind:group={tab} />
    membuat diskon
  </label>
</div>

<div class="form p-2">
  <label>harga sebelumnya</label>
  <input type="tel" bind:value={harga_sebelumnya} />
  <label>diskon (dalam persen)</label>
  <input type="tel" bind:value={diskon} />
  <label>harga setelahnya</label>
  <input type="tel" readonly bind:value={harga_setelahnya} />
  <hr class="block my-3 mb-1" />
  <label>besarnya diskon</label>
  <input type="tel" readonly bind:value={besarnya_diskon} />
</div>

<label />

<style>
  .menu label {
    @apply cursor-pointer select-none p-2 text-sm text-center;
  }
  input[type="radio"] {
    @apply hidden;
  }
  .form label {
    @apply block text-sm text-gray-600;
  }
  .form input[type="tel"] {
    @apply block w-full border border-gray-300 rounded p-2 mb-2;
  }
</style>
