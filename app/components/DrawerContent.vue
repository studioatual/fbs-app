<template lang="html">
    <GridLayout rows="auto, *" class="nt-drawer__content">
        <StackLayout row="0" class="nt-drawer__header">
            <Image class="nt-drawer__header-image" src="~/assets/img/logo2.png" />
            <!-- <Image class="nt-drawer__header-image fas t-36" src.decode="font://&#xf2bd;"></Image> -->
            <Label class="nt-drawer__header-brand" text="FBS Sistemas"></Label>
        </StackLayout>

        <ScrollView row="1" class="nt-drawer__body">
            <StackLayout>
                <GridLayout columns="auto, *" :class="'nt-drawer__list-item' + (selectedPage === 'Home' ? ' -selected': '')" @tap="onNavigationItemTap(Home)">
                    <Label col="0" text.decode="&#xf015;" class="nt-icon fas"></Label>
                    <Label col="1" text="Home" class="p-r-10"></Label>
                </GridLayout>

                <GridLayout columns="auto, *" :class="'nt-drawer__list-item' + (selectedPage === 'Clients' ? ' -selected': '')" @tap="onNavigationItemTap(Clients)">
                    <Label col="0" text.decode="&#xf0c0;" class="nt-icon fas"></Label>
                    <Label col="1" text="Clientes" class="p-r-10"></Label>
                </GridLayout>

                <GridLayout columns="auto, *" :class="'nt-drawer__list-item' + (selectedPage === 'Search' ? ' -selected': '')" @tap="onNavigationItemTap(Search)">
                    <Label col="0" text.decode="&#xf002;" class="nt-icon fas"></Label>
                    <Label col="1" text="Search" class="p-r-10"></Label>
                </GridLayout>

                <GridLayout columns="auto, *" :class="'nt-drawer__list-item' + (selectedPage === 'Featured' ? ' -selected': '')" @tap="onNavigationItemTap(Featured)">
                    <Label col="0" text.decode="&#xf005;" class="nt-icon fas"></Label>
                    <Label col="1" text="Featured" class="p-r-10"></Label>
                </GridLayout>

                <StackLayout class="hr"></StackLayout>

                <GridLayout columns="auto, *" :class="'nt-drawer__list-item' + (selectedPage === 'Settings' ? ' -selected': '')" @tap="onNavigationItemTap(Settings)">
                    <Label col="0" text.decode="&#xf013;" class="nt-icon fas"></Label>
                    <Label col="1" text="Settings" class="p-r-10"></Label>
                </GridLayout>
            </StackLayout>
        </ScrollView>
    </GridLayout>
</template>

<script>
    import Home from "./Home";
    import Clients from "./Clients";
    import Featured from "./Featured";
    import Search from "./Search";
    import Settings from "./Settings";
    import * as utils from "~/shared/utils";
    import SelectedPageService from "~/shared/selected-page-service";

    export default {
        mounted() {
            SelectedPageService.getInstance().selectedPage$
                .subscribe((selectedPage) => this.selectedPage = selectedPage);
        },
        data () {
            return {
                Home: Home,
                Clients: Clients,
                Featured: Featured,
                Search: Search,
                Settings: Settings,
                selectedPage: ""
            };
        },
        components: {
            Home,
            Clients,
            Featured,
            Search,
            Settings
        },
        methods: {
            onNavigationItemTap(component) {
                this.$navigateTo(component, {
                    clearHistory: true
                });
                utils.closeDrawer();
            }
        }
    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '~@nativescript/theme/scss/variables/blue';
    // End custom common variables

    // Custom styles

    .nt-drawer__header {
        padding: 15;
        background-size: 100% 100%;
        background: url(~/assets/img/fnd.jpg) no-repeat;
    }

    .nt-drawer__header-image {
        padding: 10;
        background-color: #fff;
    }

    .nt-drawer__header-brand {
        font-size: 20;
        font-weight: 600;
        color: #fff;
    }
</style>
