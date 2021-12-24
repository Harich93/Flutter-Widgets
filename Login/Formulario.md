# Formulario y validaciones

## Login Screen

```dart
class _LoginForm extends StatelessWidget {

  @override
  Widget build(BuildContext context) {

    final loginProvider = Provider.of<LoginProvider>(context);

    return Container(
      
      child: Form(  
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
    );
  }
}
```
## Form:

```dart
class _LoginForm extends StatelessWidget {

  @override
  Widget build(BuildContext context) {

    final loginProvider = Provider.of<LoginProvider>(context);

    return Container(
      
      child: Form(  
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
    );
  }
}
```

## _LoginButtom:

```dart
class _LoginButton extends StatelessWidget {
  const _LoginButton({
    Key? key,
    required this.loginProvider,
  }) : super(key: key);

  final LoginProvider loginProvider;

  @override
  Widget build(BuildContext context) {
    return MaterialButton(
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
      disabledColor: Colors.grey,
      elevation: 0,
      color: Colors.deepPurple,
      child: Container(
        padding: const  EdgeInsets.symmetric( horizontal: 80, vertical: 15),
        child: Text(
          loginProvider.isLoading
            ? 'Espere...'
            :'Ingresar', 
          style: const TextStyle( color: Colors.white) 
        )
      ),
      onPressed: loginProvider.isLoading ? null : () {
        
        FocusScope.of(context).unfocus(); // Quitar teclado
        loginProvider.isLoading = true;
        
        loginProvider.isValidForm() 
          ? Navigator.pushReplacementNamed(context, HomeScreen.routeName) 
          : null;
      }
    );
  }
```
