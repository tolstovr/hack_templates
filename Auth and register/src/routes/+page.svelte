<script>
    let isAuth = !true
    let authForm = {
        email: "",
        password: ""
    }

    let regForm = {
        email: "",
        name: "",
        surname: "",
        password: "",
        repeatPassword: "",
    }

    $: isPasswordMatches = regForm.password === regForm.repeatPassword

    const submitForm = (event) => {
        if (!isPasswordMatches) {
            alert("Пароли не совпадают!")
            return
        }

        const response = {
            request: isAuth ? "auth" : "reg",
            ...(isAuth ? authForm : regForm)
        }

        alert(`Final response: ${JSON.stringify(response, ",", 2)}`)
        // something
    }
</script>

<section>
    <h1>
        <span on:click={() => {isAuth = true}} class={isAuth && "active"}>Вход</span>
        и
        <span on:click={() => {isAuth = false}} class={!isAuth && "active"}>Регистрация</span>
    </h1>
    <form method="post" on:submit|preventDefault={submitForm}>
        {#if isAuth}
            <input type="text" placeholder="Электронная почта" required class="text-input" bind:value={authForm.email}>
            <input type="password" placeholder="Пароль" required class="text-input" bind:value={authForm.password}>
            <input type="submit" value="Войти">
        {:else}
            <input type="text" placeholder="Электронная почта" required class="text-input" bind:value={regForm.email}>
            <input type="text" placeholder="Имя" required class="text-input" bind:value={regForm.name}>
            <input type="text" placeholder="Фамилия" required class="text-input" bind:value={regForm.surname}>
            <input type="password" placeholder="Пароль" required bind:value={regForm.password} class="text-input">
            <input type="password" placeholder="Повтор пароля" required bind:value={regForm.repeatPassword} class="text-input">
            <span>{!isPasswordMatches ? "Пароли не совпадают" : "Пароли совпадают"}</span>
            <input type="submit" value="Зарегистрироваться">
        {/if}
    </form>
    <pre>{JSON.stringify(isAuth ? authForm : regForm, ",", 2)}</pre>
</section>

<style lang="scss">
    @import "../styles/app.scss";
    @import "../styles/form.scss";
</style>