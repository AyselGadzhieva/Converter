<template>
    <Page>
        <ActionBar title="Расстояние" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack" />
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto">
                    <TextField class="bt1" v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1" />
                    <Label class="value" :text="centimeter" row="1" col="0" />
                    <Label class="value" text="см" row="1" col="1" />
                    <Label class="value" :text="meter" row="2" col="0" />
                    <Label class="value" text="м" row="2" col="1" />
                    <Label class="value" :text="kilometer" row="3" col="0" />
                    <Label class="value" text="км" row="3" col="1" />
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
                currentValue: "см",
                meter: "",
                centimeter: "",
                kilometer: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.meter = "";
                this.centimeter = "";
                this.kilometer = "";
            },
            calculationValue(currentValue) {
                if (this.textFieldValue != "") {
                    if (this.textFieldValue == "-") {
                        alert({
                            title: "Ошибка!",
                            message: "Величина не может быть отрицательной.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear();
                        });
                    }
                    if (this.textFieldValue == "." || this.textFieldValue ==
                        "+") {
                        alert({
                            title: "Ошибка!",
                            message: "Некорректный ввод.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear();
                        });
                    }
                    switch (currentValue) {
                        case "см": {
                            this.centimeter = parseFloat(this.textFieldValue);
                            this.meter = parseFloat(this.textFieldValue) /
                            100;
                            this.kilometer =
                                parseFloat(this.textFieldValue) / 100000;
                            break;
                        }
                        case "м": {
                            this.centimeter = parseFloat(this
                                .textFieldValue) * 100;
                            this.meter = parseFloat(this.textFieldValue);
                            this.kilometer = parseFloat(this.textFieldValue) /
                                1000;
                            break;
                        }
                        case "км": {
                            this.centimeter =
                                parseFloat(this.textFieldValue) * 100000;
                            this.meter = parseFloat(this.textFieldValue) *
                                1000;
                            this.kilometer = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.meter = "";
                    this.centimeter = "";
                    this.kilometer = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "см",
                    "м",
                    "км"
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