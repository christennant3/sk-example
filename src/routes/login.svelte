<script>
    import axios from "axios";
    let email = "";
    let password = "";
    let url = "http://localhost:44314/api/User/authenticate";
    var username = "admin";
    // fetch and axios code both hit the api but dont set a cookie - must be a diffrent backend setting
    const submit = async () => {
        // let response = await fetch(
        //     "http://localhost:44314/api/User/authenticate",
        //     {
        //         method: "POST",
        //         headers: { "Content-Type": "application/json" },
        //         credentials: "include",
        //         body: JSON.stringify({
        //             username: email,
        //             password: password,
        //         }),
        //     }
        // );
        // let data = await response.json();
        // console.log(data);
        
        let e = email;
        let p = password;
        
        axios
            .post("http://localhost:44314/api/User/authenticate", {
                username: email,
                password: password,
            })
            .then(function (response) {
                let data = response.data;
                console.log(data);
             
                localStorage.setItem('t', data.token);

            })
            .catch(function (error) {
                
            });
    };
</script>

<form on:submit|preventDefault={submit}>
    <h2 class="h3 mb-3 fw-normal">Please sign in</h2>

    <div class="form-floating">
        <input
            class="form-control"
            id="floatingInput"
            placeholder="name@example.com"
            bind:value={email}
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

    <div class="checkbox mb-3">
        <label>
            <input type="checkbox" value="remember-me" /> Remember me
        </label>
    </div>
    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    <p class="mt-5 mb-3 text-muted">&copy; 2017???2022</p>
</form>
