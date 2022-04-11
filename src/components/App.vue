<template>
    <Page>
        <ActionBar title="Перевод единиц измерения" />
        <ScrollView>
            <GridLayout columns="*, *" rows="*, *, *">
                <StackLayout orientation="vertical" row="0" col="0">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/1.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Давление')" class="containerItem" text="Давление"> </Button>
                </StackLayout>
                <StackLayout orientation="vertical" row="0" col="1">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/2.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Температура')" class="containerItem" text="Температура"> </Button>
                </StackLayout>
                <StackLayout orientation="vertical" row="1" col="0">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/3.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Скорость')" class="containerItem" text="Скорость"> </Button>
                </StackLayout>
                <StackLayout orientation="vertical" row="1" col="1">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/4.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Валюта')" class="containerItem" text="Валюта"> </Button>
                </StackLayout>
                <StackLayout orientation="vertical" row="2" col="0">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/5.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Вес')" class="containerItem" text="Вес"> </Button>
                </StackLayout>
                <StackLayout orientation="vertical" row="2" col="2">
                    <AbsoluteLayout width="100" height="100">
                        <Image src="~/assets/images/6.png" stretch="aspectFill" />
                    </AbsoluteLayout>
                    <Button @tap="onItemTap('Расстояние')" class="containerItem" text="Расстояние"> </Button>
                </StackLayout>
            </GridLayout>
        </ScrollView>
    </Page>
</template>

<script>
    import Currency from "./Currency";
    import Length from "./Length";
    import Pressure from "./Pressure";
    import Speed from "./Speed";
    import Temperature from "./Temperature";
    import Weight from "./Weight";

    export default {
        components: {
            Currency,
            Length,
            Pressure,
            Speed,
            Temperature,
            Weight
        },
        methods: {
            onItemTap: function(namePage) {
                switch (namePage) {
                    case "Давление": {
                        this.$navigateTo(Pressure);
                        break;
                    }
                    case "Температура": {
                        this.$navigateTo(Temperature);
                        break;
                    }
                    case "Скорость": {
                        this.$navigateTo(Speed);
                        break;
                    }
                    case "Валюта": {
                        this.$navigateTo(Currency);
                        break;
                    }
                    case "Вес": {
                        this.$navigateTo(Weight);
                        break;
                    }
                    case "Расстояние": {
                        this.$navigateTo(Length);
                        break;
                    }

                }
            }
        },
        data() {
            return {};
        }
    };
</script>

<style scoped>
    ActionBar {
        background-color: #8a388561;
        color: white;
    }

    Button {
        color: #6c115e;
    }

    AbsoluteLayout {
        margin: 10px;
    }

    Image {
        width: 100%;}

    .select {
        width: 40%;}

    .containerItem {
        font-size: 22;
        color: #681e77;
    }
</style>