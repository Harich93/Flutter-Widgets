# Formulario y validaciones

## Form:

```dart
Form(  
        key: loginProvider.formKey,
        autovalidateMode: AutovalidateMode.onUserInteraction,
        child: Column(
          children: [
            
            // <-- Input Email -->
            TextFormField(
              autocorrect: false,
              keyboardType: TextInputType.emailAddress,
              decoration: InputDecorations.authInput(
                hintText: 'example@gmail.com',
                labelText: 'Email',
                prefixIcon: Icons.alternate_email
              ),
              onChanged: ( value ) => loginProvider.email = value,
              validator: ( value ) => Validators.email(value) ,
            ),
            
            const SizedBox( height: 30 ),
            
            // <-- Input Paswword -->
            TextFormField(
              obscureText: true,
              autocorrect: false,
              keyboardType: TextInputType.emailAddress,
              decoration: InputDecorations.authInput(
                hintText: 'Password',
                labelText: 'Contraseña',
                prefixIcon: Icons.lock_outline
              ),
              onChanged: ( value ) => loginProvider.password = value,
              validator: ( value ) => Validators.pass(value) ,
            ),

            const SizedBox( height: 30 ),

            _LoginButton(loginProvider: loginProvider)

          ],
        ),
      ),
```

## Validaciones:

```dart
class Validators {

  static String? email( String? value ) {

    String pattern = r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$';
    
    RegExp regExp  = RegExp(pattern);

    return regExp.hasMatch(value ?? '' )
      ? null
      : 'Email no válido';
  }

  static String? pass( String? value ) {
    return ( value != null && value.length >= 6 )
      ? null
      : 'Debe tener minimo 6 caracteres';
  }

}
```