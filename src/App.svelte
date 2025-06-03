<script>
  // @ts-nocheck

  let components = [
    {
      id: "cpu",
      title: "CPU",
      options: [{ price: 3399, name: "Ryzen 7800X3D" }],
    },
    {
      id: "cooler",
      title: "CPU Køler",
      options: [{ price: 289, name: "Thermalright Phantom Spirit 120 SE" }],
    },
    {
      id: "motherboard",
      title: "Bundkort",
      options: [{ price: 999, name: "GIGABYTE B650 EAGLE AX" }],
    },
  ];

  let prices = components.reduce((acc, component) => {
    acc[component.id] = 0;
    return acc;
  }, {});

  function updatePrice(category, value) {
    prices[category] = Number(value);
    prices = { ...prices }; // Trigger reactivity
  }

  $: totalPrice = Object.values(prices).reduce((acc, price) => acc + price, 0);
</script>

<div class="dropdown-container">
  <h1>Vælg produkter</h1>

  <div>
    {#each components as component}
      <div>
        <label for={component.id}>
          {component.title}
        </label>
        <select
          id={component.id}
          on:change={(e) => updatePrice(component.id, e.target.value)}
        >
          <option value="0">--- VÆLG ---</option>
          {#each component.options as option}
            <option value={option.price}>
              {option.name} - {option.price} kr
            </option>
          {/each}
        </select>
      </div>
    {/each}

    <div>
      Total pris: <span>{totalPrice}</span> kr
    </div>
  </div>
</div>
