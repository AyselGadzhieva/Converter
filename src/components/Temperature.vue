<template>
    <Page>
        <ActionBar title="Температура" />
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
                    <Label class="value" :text="celsius" row="1" col="0" />
                    <Label class="value" text="°C" row="1" col="1" />
                    <Label class="value" :text="fahrenheit" row="2" col="0" />
                    <Label class="value" text="°F" row="2" col="1" />
                    <Label class="value" :text="kelvin" row="3" col="0" />
                    <Label class="value" text="K" row="3" col="1" />
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
                currentValue: "°C",
                celsius: "",
                fahrenheit: "",
                kelvin: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.celsius = "";
                this.fahrenheit = "";
                this.kelvin = "";
            },
            calculationValue(currentValue) {
                
                if (this.textFieldValue != "") {
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
                        case "°C": {
                            this.celsius = parseFloat(this.textFieldValue);
                            this.fahrenheit =
                                (parseFloat(this.textFieldValue) * 9) / 5 +
                                32;
                            this.kelvin = parseFloat(this.textFieldValue) +
                                273.15;
                            break;
                        }
                        case "°F": {
                            this.celsius =
                                ((parseFloat(this.textFieldValue) - 32) * 5) /
                                9;
                            this.fahrenheit = parseFloat(this.textFieldValue);
                            this.kelvin = this.celsius + 273.15;
                            break;
                        }
                        case "K": {
                            this.celsius = parseFloat(this.textFieldValue) -
                                273.15;
                            this.fahrenheit = (this.celsius * 9) / 5 + 32;
                            this.kelvin = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.celsius = "";
                    this.fahrenheit = "";
                    this.kelvin = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "°C",
                    "°F",
                    "K"
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