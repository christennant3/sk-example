<script>

    let name = "";
    let email = "";
    let password = "";

    const submit = async () => {
        await fetch('http:://localhost:8000/api/register', {
            method: 'POST',
            headers: {'Content-Type':'application/json'},
            body: JSON.stringify({
                name,
                email,
                password
            })
        });
        await console.log('done');
    }
</script>

<form on:submit|preventDefault={submit}>
    <h2 class="h3 mb-3 fw-normal">Register</h2>

    <div class="form-floating">
        <input
            bind:value={name}
            type="text"
            class="form-control"
            id="floatingInput"
        />
        <label for="floatingInput">Name</label>
    </div>

    <div class="form-floating">
        <input
            bind:value={email}
            type="email"
            class="form-control"
            id="floatingInput"
        />
        <label for="floatingInput">Email address</label>
    </div>
    <div class="form-floating">
        <input
            type="password"
            class="form-control"
            id="floatingPassword"
            placeholder="Password"
            bind:value={password}
        />
        <label for="floatingPassword">Password</label>
    </div>
    <br /><br />
    <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
</form>
