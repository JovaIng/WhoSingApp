Proyecto final: reconocimiento de música.
Por Omar Jovany Hernández Sánchez (344187).

Descripción: 
WhoSingApp reconoce las canciones si se encuentran en su base de datos, haciendo la búsqueda de forma recursiva, este muestra el resultado, indicando el nombre y el artista si se encuentra en la base de datos, además de recomendar artistas relacionados a raíz de esa búsqueda.

Estas son las funciones principales:

% reconocer canción, al darle un fragmento de letra.

reconocer(LstFragmento,Letra,Titulo,Artista,Genero):-
    findall(X,cancion(Titulo,Artista,Genero,X),LstLetras),
       busca(LstFragmento, Letra, Titulo, Artista,Genero, LstLetras).

la función busca, es la que hace todo el trabajo, buscando en la lista que le entrega findall la letra que coincida con el fragmento proporcionado por el usuario:

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image1.png" alt="image1">

% mostrar todos los artistas de los géneros especificados en una lista.

artistasDeLosGeneros([],[]).
artistasDeLosGeneros([X|Y],LstArtistas):-
    findall(Artista,artistaDelGenero(X,Artista),Lst),
       artistasDeLosGeneros(Y,LstAux), concat(Lst,LstAux,LstArtistas).

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image2.png" alt="image2">

% mostrar el listado completo de todos los artistas registrados.

mostrarTodosLosArtistas():- findall(Artista, cancion(_,Artista,_,_),LstAux), eliminaRepetidos(LstAux,LstArtistas),imprimirArtistas(LstArtistas).

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image3.png" alt="image3">

% mostrar artista del genero especificado.

artistaDelGenero(Genero,Artista):-
    cancion(_,Artista,LstGeneros,_), mismoConjunto([Genero],LstGeneros).

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image4.png" alt="image4">

% Los predicados que contienen la información de las canciones, tienen la siguiente estructura:

cancion(Titulo, Artista, LstGeneros, LstLetra).

Para generar los predicados "cancion" se creo una aplicación en C# con Visual Studio; este busca la letra y el genero al indicar el nombre de la canción y artista, permitiendo con ello la rápida generación de los predicados sin tener qué escribirlos a pie.

Ejemplo:

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image5.JPG" alt="image5">

% Predicado generado con aplicación

<img src="https://github.com/JovaIng/WhoSingApp/blob/master/images/image6.png" alt="image6">


Generador de predicados (.exe): http://www.mediafire.com/file/jnfh5u38qkqeomw/WhoSingApp.exe/file
Código fuente archivo prolog: http://www.mediafire.com/file/yn7x9i16895adf5/WhoSingApp.zip/file
