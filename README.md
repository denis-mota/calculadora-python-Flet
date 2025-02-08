import flet as ft

def main(page: ft.Page):
    page.title ="calculador simples"
    page.window.width = 400
    page.window.height = 500


    #campo de entrada para os numeros
    num1 = ft.TextField(label="numero 1", keyboard_type=ft.KeyboardType.NUMBER)
    num2 = ft.TextField(label="numero 2", keyboard_type=ft.KeyboardType.NUMBER)

    #texto para exibir o resultado
    resultado = ft.Text("o resultado aparecerá aqui.")

    #função para calcular
    def calcular(e):
        try:
            a = float(num1.value)
            b = float(num2.value)

            if e.control.data == "soma":
                resultado.value = f"resultado: {a + b}"
            elif e.control.data == "subtracao":
                resultado.value = f"resultado: {a - b}"
            elif e.control.data == "multiplicacao":
                resultado.value = f"resultado: {a * b}"
            elif e.control.data == "divisao":
                if b == 0:
                    resultado.value = "Erro: divisão por zero!"
                else:
                    resultado.value = f"resultado: {a / b}"

        except ValueError:
            resultado.value = "Erro: digite numeros validos!"


        page.update()  #atualiza a pagina

    #botoes para calcular
    botoes = ft.Row([
        ft.ElevatedButton("+", on_click=calcular, data="soma"),
        ft.ElevatedButton("-", on_click=calcular, data="subtracao"),
        ft.ElevatedButton("*", on_click=calcular, data="multiplicacao"),
        ft.ElevatedButton("/", on_click=calcular, data="divisao")
    ], alignment=ft.MainAxisAlignment.CENTER)

    #adicionando elementos na pagina
    page.add(num1, num2, botoes, resultado)

ft.app(target=main, view=ft.FLET_APP)
