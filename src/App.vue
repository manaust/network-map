<template>
  <button @click="addNode">Add node</button>
  <div style="width: 100%; height: 75%" ref="network" />
</template>

<script setup>
import { onMounted, reactive, ref, watchEffect } from "vue";
import { Network } from "vis-network";

import IconExtender from "./components/icons/IconExtender.svg";
import IconMobile from "./components/icons/IconMobile.svg";
import IconTablet from "./components/icons/IconTablet.svg";
import IconDesktop from "./components/icons/IconDesktop.svg";
import IconNetwork from "./components/icons/IconNetwork.svg";

const network = ref(null);
const data = reactive({
  nodes: [],
  edges: [],
});

const LENGTH_MAIN = 250,
  LENGTH_SUB = 50,
  WIDTH_SCALE = 3;

const htmlTitle = (html) => {
  const container = document.createElement("div");
  container.innerHTML = html;
  return container;
};

onMounted(() => {
  data.nodes.push({
    id: 1,
    label: "Hallway",
    group: "switch",
    value: 32,
    font: "20px arial #0a0098",
  });

  data.nodes.push({
    id: 2,
    label: "Office",
    group: "internet",
    value: 32,
    font: "20px arial #0a0098",
  });

  data.edges.push({
    from: 1,
    to: 2,
    length: LENGTH_MAIN,
    width: WIDTH_SCALE,
    label: "0.71 mbps",
    color: "#e14c9d",
    title: htmlTitle(
      "Go wild <'span style='display: inline-block; animation: be-tacky 5s ease-in-out alternate infinite; margin: 5px;'>!<'/span>"
    ),
  });

  // group around 1
  data.nodes.push({
    id: 103,
    label: "iPhone Tommy",
    group: "mobile",
    value: 4,
  });

  data.edges.push({
    from: 1,
    to: 103,
    length: LENGTH_SUB,
    color: "#16869a",
    width: WIDTH_SCALE,
  });

  data.nodes.push({
    id: 104,
    label: "Galaxy S5 Lisa",
    group: "mobile",
    value: 4,
  });

  data.edges.push({
    from: 1,
    to: 104,
    length: LENGTH_SUB,
    color: "#9739c3",
    width: WIDTH_SCALE,
  });

  data.nodes.push({
    id: 105,
    label: "Tablet Noah",
    group: "tablet",
    value: 4,
  });

  data.edges.push({
    from: 1,
    to: 105,
    length: LENGTH_SUB,
    color: "#9739c3",
    width: WIDTH_SCALE,
    dashes: true,
  });

  data.nodes.push({
    id: 106,
    label: "Acer 192.158.1.38",
    group: "desktop",
    value: 4,
  });

  data.edges.push({
    from: 1,
    to: 106,
    length: LENGTH_SUB,
    color: "#e14c9d",
    width: WIDTH_SCALE,
    dashes: true,
  });

  // group around 2
  data.nodes.push({
    id: 201,
    label: "Laptop Anna",
    group: "desktop",
    value: 4,
  });

  data.edges.push({
    from: 2,
    to: 201,
    length: LENGTH_SUB,
    color: "#e14c9d",
    width: WIDTH_SCALE,
  });

  const options = {
    nodes: {
      scaling: {
        min: 16,
        max: 32,
      },
      font: "14px arial #0a0098",
    },
    edges: {
      color: "gray",
      smooth: false,
    },
    physics: {
      barnesHut: { gravitationalConstant: -30000 },
      stabilization: { iterations: 2500 },
    },
    groups: {
      switch: {
        shape: "image",
        image: IconExtender,
      },
      desktop: {
        shape: "image",
        image: IconDesktop,
      },
      mobile: {
        shape: "image",
        image: IconMobile,
      },
      tablet: {
        shape: "image",
        image: IconTablet,
      },
      internet: {
        shape: "image",
        image: IconNetwork,
      },
    },
  };

  watchEffect(() => {
    console.log("watchEffect triggered");
    new Network(network.value, data, options);
  });
});

const addNode = () => {
  console.log("Adding node...");
  data.nodes.push({
    id: 109,
    label: "Laptop Anna",
    font: "14px arial blue",
    group: "desktop",
    value: 4,
  });

  data.edges.push({
    from: 1,
    to: 109,
    length: LENGTH_SUB,
    color: "red",
    width: WIDTH_SCALE,
    dashes: true,
  });
};
</script>
