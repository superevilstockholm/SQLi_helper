<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container">
            <RouterLink class="navbar-brand d-flex flex-row align-items-center gap-2 fw-bold" to="/">
                <span class="text-danger d-flex flex-row align-items-center gap-1">
                    <img style="height: 25px; width: auto;" src="@/assets/sql-injection-icon.png" alt="sqli icon from flaticon by nangicon">
                    SQLi
                </span>
                Helper
            </RouterLink>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse fw-normal" style="font-size: 0.9rem;" id="navbarNav">
                <ul class="navbar-nav ms-auto me-0 text-center gap-3">
                    <li class="nav-item">
                        <RouterLink class="nav-link active" aria-current="page" to="/">Dashboard</RouterLink>
                    </li>
                    <li class="nav-item">
                        <RouterLink class="nav-link" to="/docs">Docs</RouterLink>
                    </li>
                    <li class="nav-item">   
                        <a class="nav-link" href="https://www.github.com/superevilstockholm" target="_blank">GitHub</a>
                    </li>
                    <li class="nav-item me-0 pe-0">
                        <RouterLink class="nav-link pe-0 me-0" to="/patreon">Donation</RouterLink>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');
* {
    font-family: 'Inter';
}
</style>