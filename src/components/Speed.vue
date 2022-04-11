<template>
    <Page>
        <ActionBar title="Скорость" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack" />
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto, auto">
                    <TextField class="bt1" v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1"/>
                    <Label class="value" :text="kmvch" row="1" col="0" />
                    <Label class="value" text="км/ч" row="1" col="1" />
                    <Label class="value" :text="mvch" row="2" col="0" />
                    <Label class="value" text="м/ч" row="2" col="1" />
                    <Label class="value" :text="kmvc" row="3" col="0" />
                    <Label class="value" text="км/с" row="3" col="1" />
                    <Label class="value" :text="mvc" row="4" col="0" />
                    <Label class="value" text="м/с" row="4" col="1" />
                </GridLayout>
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    export default {
        data() {
            return {
                textFieldValue: "",
                currentValue: "км/ч",
                kmvch: "",
                mvch: "",
                kmvc: "",
                mvc: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.kmvch = "";
                this.mvch = "";
                this.kmvc = "";
                this.mvc = ""
            },
            calculationValue(currentValue) {

                if (this.textFieldValue != "") {
                    if (this.textFieldValue == "-") {
                        alert({
                            title: "Ошибка!",
                            message: "Величина не может быть отрицательной.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    if (this.textFieldValue == "." || this.textFieldValue == "+") {
                        alert({
                            title: "Ошибка!",
                            message: "Некорректный ввод.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    switch (currentValue) {
                        case "км/ч": {
                            this.kmvch= parseFloat(this.textFieldValue);
                            this.mvch = parseFloat(this.textFieldValue) *
                                1000;
                            this.kmvc = parseFloat(this.textFieldValue) *
                                0.0003;
                            this.mvc = parseFloat(this.textFieldValue) / 3.6;
                            break;
                        }
                        case "м/ч": {
                            this.kmvch= parseFloat(this.textFieldValue) * 0.001;
                            this.mvch = parseFloat(this.textFieldValue);
                            this.kmvc = parseFloat(this.textFieldValue) *
                                0.00000027777;
                            this.mvc = parseFloat(this.textFieldValue) * 0.0003;
                            break;
                        }
                        case "км/с": {
                            this.kmvch= parseFloat(this.textFieldValue) * 3600;
                            this.mvch = parseFloat(this.textFieldValue) * 3600000;
                            this.kmvc = parseFloat(this.textFieldValue);
                            this.mvc = parseFloat(this.textFieldValue) * 1000;
                            break;
                        }
                        case "м/с": {
                            this.kmvch= parseFloat(this.textFieldValue) * 3.6;
                            this.mvch = parseFloat(this.textFieldValue) * 3600;
                            this.kmvc = parseFloat(this.textFieldValue) * 0.001;
                            this.mvc = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.kmvch = "";
                    this.mvch = "";
                    this.kmvc = "";
                    this.mvc = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "км/ч",
                    "м/ч",
                    "км/с",
                    "м/с"
                ]).then(result => {
                    if (result != "Отменить") {
                        this.currentValue = result;
                        this.calculationValue(this.currentValue);
                    }
                });
            }
        }
    };
</script>

<style>

</style>