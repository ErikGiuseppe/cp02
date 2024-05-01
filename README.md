# cp02

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class Contato {
  String nome;
  String email;
  bool favorito;

  Contato({required this.nome, required this.email, this.favorito = false});
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Lista de Contatos',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ListaContatos(),
    );
  }
}

class ListaContatos extends StatefulWidget {
  @override
  _ListaContatosState createState() => _ListaContatosState();
}

class _ListaContatosState extends State<ListaContatos> {
  List<Contato> contatos = [
    Contato(nome: 'Hugo', email: 'hugo@gmail.com'),
    Contato(nome: 'Ramoz', email: 'ramoz@gmail.com'),
    Contato(nome: 'Lucas', email: 'lucas@gmail.com'),
    Contato(nome: 'Guilherme', email: 'guilherme@gmail.com'),
    Contato(nome: 'Sistema', email: 'sistema@gmail.com'),
  ];

  int _contatosFavoritos() {
    return contatos.where((contato) => contato.favorito).length;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Row(
          children: [
            Text('Lista de Contatos'),
            SizedBox(width: 8),
            Container(
              padding: EdgeInsets.all(4),
              child: Text(
                '${_contatosFavoritos()}',
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 12,
                ),
              ),
            ),
          ],
        ),
      ),
      body: ListView.builder(
        itemCount: contatos.length,
        itemBuilder: (context, index) {
          return ListTile(
            leading: CircleAvatar(
              backgroundImage: NetworkImage('https://i.pravatar.cc/150?img=1'),
            ),
            title: Text(contatos[index].nome),
            subtitle: Text(contatos[index].email),
            trailing: IconButton(
              icon: contatos[index].favorito
                  ? Icon(Icons.favorite, color: Colors.red)
                  : Icon(Icons.favorite_border),
              onPressed: () {
                setState(() {
                  contatos[index].favorito = !contatos[index].favorito;
                });
              },
            ),
          );
        },
      ),
    );
  }
}
