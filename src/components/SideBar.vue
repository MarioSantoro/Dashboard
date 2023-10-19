<template>
    <nav>
        <div class="title mb-4">
            <h5>- Dashbool -</h5>
        </div>

        <div class="profile d-flex align-items-center">
            <div class="image-profile me-3">
                <img src="../assets/WhatsApp Image 2023-09-09 at 19.22.36.jpeg" alt="">
            </div>
            <div class="name-user">
                <h6 class="m-0">Welcome</h6>
                <p class="m-0">Mario Santoro</p>
            </div>
        </div>

        <div class="menu">
            <p class="text-uppercase mt-3 mb-2">General</p>
            <div class="wrapper">
            </div>
            <div class="option">
                <div class="accordion accordion-flush" id="accordionFlushExample" v-for="option in  listItem ">
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
                                :data-bs-target="'#' + option.number" aria-expanded="false" :aria-controls="option.number">
                                <i :class="option.icon"></i> {{ option.text }}
                            </button>
                        </h2>
                        <div :id="option.number" class="accordion-collapse collapse"
                            data-bs-parent="#accordionFlushExample">
                            <ul class="accordion-body list-unstyled">
                                <li>Dashboard 1</li>
                                <li>Dashboard 2</li>
                                <li>Dashboard 3</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>
<script>
export default {
    data() {
        return {
            listItem: [
                {
                    number: 'flush-collapseOne',
                    icon: 'fa-solid fa-house me-3',
                    text: 'Home'
                },
                {
                    number: 'flush-collapseTwo',
                    icon: 'fa-solid fa-map-location-dot me-3',
                    text: 'Maps'
                },
                {
                    number: 'flush-collapseThree',
                    icon: 'fa-solid fa-gear me-3',
                    text: 'Config'
                },
                {
                    number: 'flush-collapseFour',
                    icon: 'fa-solid fa-envelope me-3',
                    text: 'Contacts'
                },
            ]
        }
    }
}
</script>
<style lang="scss" scoped>
nav {
    background-color: #2A4054;
    width: 12%;
    height: 100vh;
    padding: .66rem .44rem;
    color: white;

    div.profile {
        div.image-profile {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            overflow: hidden;
            border: 3px solid white;

            img {
                height: 100%;
                width: 100%;
                object-fit: cover;
            }
        }
    }

    div.menu {
        div.wrapper {
            height: 3px;
            background-color: white;
        }

        .accordion {
            --bs-accordion-bg: none;
            --bs-accordion-btn-color: white;
            --bs-accordion-btn-focus-border-color: none;
            --bs-accordion-btn-focus-box-shadow: none;
            --bs-accordion-btn-icon: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='FFF'%3e%3cpath fill-rule='evenodd' d='M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z'/%3e%3c/svg%3e");
            --bs-accordion-btn-active-icon: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='FFFFFF'%3e%3cpath fill-rule='evenodd' d='M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z'/%3e%3c/svg%3e");
            --bs-accordion-border-width: none;
            --bs-accordion-active-color: white;
            --bs-accordion-active-bg: none;
        }
    }
}
</style>