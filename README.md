# Minha Carteira

Abra `index.html` no navegador ou execute `python -m http.server 8080` e acesse `http://localhost:8080`.

## Persistência para estudar

O projeto usa `localStorage`: um armazenamento local do navegador que permanece após recarregar ou fechar a página. Aqui ele funciona como persistência dos dados do formulário, sem servidor ou banco de dados.

- Chave: `minhaCarteira.profile.v1`.
- Conteúdo: nome, curso, CPF, nascimento, matrícula, validade e estado expandido/recolhido.
- `saveProfile()` transforma o objeto em JSON e salva com `setItem()`.
- `loadProfile()` lê com `getItem()`, interpreta com `JSON.parse()` e verifica o formato antes de restaurar.
- A matrícula é gerada uma única vez. Editar os dados mantém o número; somente **Sortear matrícula agora** gera outro.
- **Meus dados**, a seta de voltar e **Sair** abrem o formulário sem apagar o que foi salvo. As alterações do formulário são gravadas em **Salvar e continuar**.
- Se o armazenamento estiver bloqueado ou cheio, a tela informa que os dados só durarão na sessão.

Para inspecionar, abra as ferramentas de desenvolvedor e procure **Application → Local Storage**. No console:

```js
// Ler o objeto salvo.
JSON.parse(localStorage.getItem('minhaCarteira.profile.v1'))

// Apagar o perfil para testar o primeiro acesso novamente.
localStorage.removeItem('minhaCarteira.profile.v1')
location.reload()
```

O armazenamento pertence à origem (protocolo, domínio e porta). Trocar `localhost` por `127.0.0.1`, mudar de porta ou usar outro navegador cria um armazenamento separado. Em URLs `file://`, a persistência varia entre navegadores; prefira o servidor local para estudar.

Não há expiração automática, sincronização entre dispositivos ou cache de arquivos/offline. Limpar os dados do site remove o perfil. Use dados fictícios nos estudos: `localStorage` não criptografa as informações.
