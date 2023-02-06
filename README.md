# Boolean-Logic-Interpreter-in-Python-
var = {}
def evaluate_expression(expression):
    if expression in var:
        return var[expression]
    if expression == 'T':
        return True
    if expression == 'F':
        return False
    if expression.startswith('¬'):
        return not evaluate_expression(expression[1:])
    for operator in ('∧', '∨'):
        if operator in expression:
            x, y = expression.split(operator)
            x = evaluate_expression(x)
            y = evaluate_expression(y)
            if operator == '∧':
                return x and y
            if operator == '∨':
                return x or y
    raise ValueError('Invalid expression: ' + expression)
def handle_command(command):
    if command.startswith('let '):
        variable, value = command[4:].split(' = ')
        var[variable] = evaluate_expression(value)
        print(f'{variable}: {value}')
    else:
        result = evaluate_expression(command)
        print(f'{result}')
while True:
    command = input('λ> ')
    if command == 'exit':
        break
    try:
        handle_command(command)
    except Exception as e:
        print(f'Error: {e}')
