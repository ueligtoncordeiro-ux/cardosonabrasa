# Cardoso na Brasa

Site em HTML estatico para publicacao no GitHub Pages.

## Arquivos

- `index.html`: arquivo principal publicado pelo GitHub Pages.
- `cardoso_na_brasa_v21.html`: copia versionada do HTML original.

## Publicacao

O GitHub Pages deve usar a branch `main` e a pasta raiz (`/`).

## Admin com Firebase Auth

O painel admin usa Firebase Authentication por e-mail/senha. Para ativar:

1. No Firebase Console, crie/ative um app Web do projeto `cardoso-na-brasa`.
2. Copie o `apiKey` do objeto `firebaseConfig`.
3. Em `index.html`, substitua `COLE_AQUI_A_API_KEY_DO_FIREBASE` pelo `apiKey`.
4. Em Authentication > Sign-in method, ative Email/Password.
5. Em Authentication > Users, crie o usuario admin.
6. Em Authentication > Settings > Authorized domains, adicione `ueligtoncordeiro-ux.github.io`.
7. Em Realtime Database > Rules, use regras como:

```json
{
  "rules": {
    "config": {
      ".read": true,
      ".write": "auth != null && auth.token.email == 'SEU_EMAIL_ADMIN_AQUI'"
    }
  }
}
```

Troque `SEU_EMAIL_ADMIN_AQUI` pelo e-mail criado no Firebase Auth.

## Firebase Storage

As imagens do cardapio devem ficar no Firebase Storage, nao em base64 no
Realtime Database. O projeto inclui `storage.rules` e `firebase.json` para
publicar as regras oficiais do Storage.

Para publicar via CLI:

```bash
npx firebase-tools login
npx firebase-tools deploy --only storage --project cardoso-na-brasa
```

Ou cole o conteudo de `storage.rules` no Firebase Console em
Storage > Rules > Publish.
