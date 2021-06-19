<h1 align="center">
 <img alt="Ignite Logo" src="https://github.com/Leozerassauro/ignite-react-native-todos/blob/main/github/banner.png" width="1000" />
    <br>
    Desafio 01 - Conceitos do React Native
</h1>

<p align="center">
   <a href="https://www.linkedin.com/in/leonardo-girardi-494958171/">
    <img alt="Made by Rocketseat" src="https://img.shields.io/badge/made%20by-Leonardo Girardi-%2304D361">
  </a>
  
  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/Leozerassauro/ignite-react-native-todos.svg">

  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/Leozerassauro/ignite-react-native-todos">

  <img alt="License" src="https://img.shields.io/badge/license-MIT-%2304D361">
</p>

<p align="center">
  <a href="#computer-sobre-o-desafio">Desafio</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#mag_right-testes">Testes</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#mortar_board-desafio-concluído">Desafio concluído</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#rocket-tecnologias">Tecnologias</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-license">License</a>
</p>

 ## :computer: Sobre o desafio
<p>
  Nesse desafio, você deverá criar uma aplicação para treinar o que aprendeu até agora no React Native.

  Essa será uma aplicação de lembrete de tarefas, onde você vai treinar um pouco mais sobre manipulação do estado no React.
  As funcionalidades do aplicativo são:

  - Adicionar uma nova tarefa
  - Remover uma tarefa
  - Marcar e desmarcar uma tarefa como concluída
</p>
</br>

<p align="center">
  <img src="https://github.com/Leozerassauro/ignite-react-native-todos/blob/main/github/todo-app.png" alt="Todo App" width="350" />
</p>

<p>

  ### pages/Home.tsx

  Essa é a página do aplicativo. Aqui estão todas as funções que serão responsáveis pelo gerenciamento das tarefas no App e você deve implementar as funcionalidades. São elas:

  - **handleAddTask:** Essa função deve receber o nome de uma tarefa e adicionar essa tarefa no estado no seguinte formato:

    ```tsx
    interface Task {
      id: number;
      title: string;
      done: boolean;
    }
    ```

    Ao receber o nome da tarefa na função, é importante que você verifique se esse nome é uma `string` válida. Isto é, o valor recebido **deve** ser diferente de uma `string` vazia.

    Para os valores da tarefa, você pode gerar um `id` aleatório usando o método `new Date().getTime()` e a propriedade `done` deve sempre ser iniciada com o valor `false`.
    Lembre-se também de manter as tarefas já existentes na listagem, apenas adicionando a nova tarefa. 

  - **handleMarkTaskAsDone:** Essa função deve receber o `id` de uma tarefa e alterar a propriedade `done` para o inverso do seu valor, ou seja, altere para `true` caso esteja `false` ou altere para `false` caso esteja `true`. 
  Lembre que você deve usar o conceito de imutabilidade sempre que alterar a informação de um estado. Ou seja, ao alterar a propriedade `done` de uma tarefa, não faça isso diretamente no estado `tasks`, salve a lista alterada em uma nova variável antes de salvar no estado.
  - **handleRemoveTask:** Como o próprio nome diz, essa função irá remover uma tarefa que possua o `id` igual ao `id` recebido. Para isso, você pode usar o método `filter`, criar uma nova lista com a tarefa removida a partir disso e salvar a informação no estado.

  ### components/TodoInput.tsx

Esse é o componente de input onde serão digitados os nomes das tarefas que serão adicionadas. Ao lado do input, existe um botão que adiciona o conteúdo digitado no input na lista de tarefas.

Nesse arquivo temos o estado `task` que deverá ser usado na propriedade `value` do componente `TextInput` e a função `setTask` que deve ser usada na propriedade `onChangeText` também do `TextInput`.

Você deve implementar a função que existe no arquivo que é:

- **handleAddNewTask**: Essa função deve ser chamada quando o botão `TouchableOpacity` for pressionado ou quando a tecla `enter` do teclado for pressionada (use a propriedade `onSubmitEditing` do `TextInput` para isso).
Essa função deve chamar a função `addTask` (recebida nas propriedades do componente) passando o estado `task` como argumento. Lembre de limpar o estado `task` sempre que uma nova `task` for adicionada.

### components/MyTaskList.tsx

Esse componente irá exibir a listagem de `tasks` adicionadas. Nesse arquivo, você deverá fazer o uso das propriedades `onLongPress` e `onPress` recebidas pelo componente.

Ambas são funções e devem ser chamadas no botão `TouchableOpacity` passando o `id` do `item` na lista. Para isso, lembre-se de chamar a função corretamente. 

Exemplo:

```tsx
ERRADO:
<TouchableOpacity 
  onPress={onPress(item.id)} 
  onLongPress={onLongPress(item.id)} 
>
 <Text>Botão</Text>
</TouchableOpacity>

CERTO:
<TouchableOpacity 
  onPress={() => onPress(item.id)} 
  onLongPress={() => onLongPress(item.id)} 
>
 <Text>Botão</Text>
</TouchableOpacity>
```

Além disso, você deve também aplicar as estilizações (propriedade `style`) no `TouchableOpacity`, `View` e `Text` para que exiba o item da tarefa corretamente quando marcado e quando desmarcado. Você pode usar a propriedade `done` do `item` na listagem para aplicar a estilização correta.

Caso a propriedade `done` esteja como `true`, você deve aplicar as seguintes estilizações:

- No componente `TouchableOpacity` deve-se aplicar a estilização `styles.taskButtonDone`;
- No componente `View` deve-se aplicar a estilização `styles.taskMarkerDone`;
- No componente `Text` deve-se aplicar a estilização `styles.taskTextDone`.

Caso a propriedade `done` esteja como `false`, você deve aplicar as seguintes estilizações:

- No componente `TouchableOpacity` deve-se aplicar a estilização `styles.taskButton`;
- No componente `View` deve-se aplicar a estilização `styles.taskMarker`;
- No componente `Text` deve-se aplicar a estilização `styles.taskText`.
</p>

## :mag_right: Testes

<p>

  ### Testes TodoInput

- **should be able to submit the input text by "submitEditing" event**:

    Para que esse teste passe, você deve permitir que a propriedade `submitEditing` do componente `TodoInput` esteja chamando a função `handleAddNewTask` e que essa função esteja implementada de acordo com o que foi descrito acima (você pode voltar [clicando aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d));

- **should be able to submit the input text by addButton**:

    Para que esse teste passe, você deve permitir que a propriedade `onPress` do botão ao lado do input esteja chamando a função `handleAddNewTask` e que essa função esteja implementada de acordo com o que foi descrito acima (você pode voltar [clicando aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d)).

### Testes MyTasksList

- **should be able to render all tasks:**

    Para que esse teste passe, você deve permitir que o componente `MyTasksList` receba as tarefas pela propriedade `tasks` e faça a listagem na `FlatList`. Por padrão, o template já deve ter esse teste passando;

- **should be able to handle "longPress" event:**

    Para que esse teste passe, você deve permitir que a propriedade `onLongPress` do `TouchableOpacity` na `FlatList` chame a função `onLongPress` recebida nas propriedades do componente passando o `id` da tarefa de acordo com o que foi descrito acima (você pode voltar [clicando aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d));

- **should be able to handle "press" event:**

    Para que esse teste passe, você deve permitir que a propriedade `onPress` do `TouchableOpacity` na `FlatList` chame a função `onPress` recebida nas propriedades do componente passando o `id` da tarefa de acordo com o que foi descrito acima (você pode voltar [clicando aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d)).

### Testes Home

- **should be able to render new added tasks:**

    Para que esse teste passe, você deve permitir que uma nova tarefa seja adicionada na listagem ao preencher com o conteúdo no input e confirmar com o `onSubmitEditing` ou com o `onPress` do componente TodoInput. É necessário também que você tenha implementado corretamente a função `handleAddTask` de acordo com que foi [descrito aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).

- **should not be able to add an empty task:**

    Para que esse teste passe, você deve adicionar uma nova tarefa apenas se ela possuir um título válido, de acordo com o que é [descrito aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).

- **should be able to render tasks as done and undone:**

    Para que esse teste passe, você deve colocar corretamente as estilizações das tarefas na listagem do componente `MyTasksList` de acordo com o que foi descrito [nessa seção](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d) além de ter chamado corretamente a função `onPress` recebida no componente na propriedade `onPress` do `TouchableOpacity` como é [descrito aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).
    Você precisa também implementar corretamente a função `handleMarkTaskAsDone` do componente `Home.tsx` seguindo [essas dicas](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).

- **should be able to remove tasks by "longPress" event:**

    Para que esse teste passe, você deve permitir a propriedade `onLongPress` do botão `TouchableOpacity` no componente `MyTasksList` chame a função `onLongPress` recebida pelas propriedades seguindo [essas dicas](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).
    É importante que você tenha também implementado corretamente a função `handleRemoveTask` do componente `Home.tsx` de acordo com o que é [descrito aqui](https://www.notion.so/Desafio-01-Conceitos-do-React-Native-424de969f3274ed5b9b49534b288a04d).
</p>

## :mortar_board: Desafio concluído
<p align="center">
  <img src="https://github.com/Leozerassauro/ignite-react-native-todos/blob/main/github/challenge.gif" alt="Todo App" />
</p>
</br>

</br>

## :rocket: Tecnologias

- [React Native](https://github.com/facebook/react-native)
- [Typescript](https://github.com/microsoft/TypeScript)

## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/Leozerassauro/ignite-react-native-todos/blob/main/LICENSE) for more information.

---

Made with ♥ by Leonardo Girardi :wave: [Get in touch!](https://www.linkedin.com/in/leonardo-girardi-494958171/)


