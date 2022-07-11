<script>
    import { initializeApp } from "firebase/app";
    import { getFirestore, collection, addDoc } from "firebase/firestore";
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
    </Nav>

    <Editor bind:value={textContent} />
</div>
