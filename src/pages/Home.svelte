<script>
    import { initializeApp } from "firebase/app";
    import {
        getFirestore,
        collection,
        addDoc,
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

    let textContent = "";

    async function save() {
        try {
            const docRef = await addDoc(collection(db, "pastes"), {
                content: textContent,
            });
            window.location.href = `/${docRef.id}`;
        } catch {
            alert(
                "Something went wrong while saving the paste, please try again!"
            );
        }
    }
</script>

<div class="flex flex-col h-full">
    <Nav>
        <NavItem
            title="Save"
            disabled={textContent.length === 0}
            on:click={save}
        />

        <NavItem title="About" href="https://github.com/emarforio/paste" />
    </Nav>

    <Editor bind:value={textContent} />
</div>
