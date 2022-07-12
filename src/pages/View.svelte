<script lang="ts">
  export let id: string;

  import { initializeApp } from "firebase/app";
  import {
    getFirestore,
    doc,
    getDoc,
    connectFirestoreEmulator,
  } from "firebase/firestore";
  import Nav from "../lib/Nav.svelte";
  import NavItem from "../lib/NavItem.svelte";
  import Editor from "../lib/Editor.svelte";

  // Your web app's Firebase configuration
  const firebaseConfig = {
    apiKey: "AIzaSyCtQEuYRI9SLdhdg0N96quzatPaFDzIDDE",
    authDomain: "paste-689b2.firebaseapp.com",
    projectId: "paste-689b2",
    storageBucket: "paste-689b2.appspot.com",
    messagingSenderId: "239146198884",
    appId: "1:239146198884:web:39bf57e2b5da5203137c71",
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  // Connect emulators in dev
  if (
    window.location.hostname === "localhost" ||
    window.location.hostname === "127.0.0.1"
  ) {
    console.log("Local dev env, using emulators");
    connectFirestoreEmulator(db, "localhost", 8080);
  }

  async function load() {
    const pasteRef = await getDoc(doc(db, "pastes", id));
    if (!pasteRef.exists()) {
      throw Error("Paste does not exist");
    }

    const data = pasteRef.data();
    if (!data?.content || typeof data.content != "string") {
      throw Error("Invalid paste content");
    }

    return data.content;
  }

  let textContentPromise = load();
</script>

<div class="flex flex-col h-full">
  <Nav>
    <NavItem title="Home" href="/" />

    <NavItem title="About" href="https://github.com/emarforio/paste" />
  </Nav>

  {#await textContentPromise}
    <Editor value="Loading.." readonly />
  {:then textContent}
    <Editor value={textContent} readonly />
  {:catch error}
    <Editor value={error.message} readonly />
  {/await}
</div>
