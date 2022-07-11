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
        apiKey: "AIzaSyDwSgGiZLjsMu5wExYn3NxH_Iomu6moMNc",
        authDomain: "paste-c09d8.firebaseapp.com",
        projectId: "paste-c09d8",
        storageBucket: "paste-c09d8.appspot.com",
        messagingSenderId: "343169697356",
        appId: "1:343169697356:web:935b315292d0aa0f4596e9",
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
    </Nav>

    {#await textContentPromise}
        <Editor value="Loading.." readonly />
    {:then textContent}
        <Editor value={textContent} readonly />
    {:catch error}
        <Editor value={error.message} readonly />
    {/await}
</div>
