# LumeLib 4.0

Biblioteca digital pessoal, leitor EPUB/PDF/TXT, catálogo, quadros de leitura e estúdio local de estudo com referências de origem. Projeto web/PWA com APK Android experimental.

## Arquivos

- `index.html`: aplicação standalone com JSZip incorporado.
- `icon-192.png`, `icon-512.png`: ícone azul-escuro com livro e pena.
- `manifest.webmanifest`, `sw.js`: arquivos de instalação PWA por HTTPS.
- `supabase-setup.sql`: tabelas, políticas RLS e bucket privado opcionais.
- `builders/build_apk.py`, `builders/icon_resources.py`, `builders/verify_apk.py`: gerador e verificadores do APK. São ferramentas experimentais que não substituem o Android Gradle Plugin.

## Login por e-mail e armazenamento

A implementação usa Supabase Auth (e-mail/senha), Supabase Storage (`lumelib-files`) e PostgREST para metadados. Depende de projeto ativo configurado na interface. Uma chave pública de acesso (anon/publishable) não é uma chave secreta; **nunca use `service_role`** no código distribuído. Ative verificação de e-mail, SMTP confiável para uso continuado e política de quotas. RLS no `supabase-setup.sql` isola os dados por usuário.

**Observação de privacidade:** os arquivos são enviados ao seu próprio projeto de nuvem somente após conexão da conta e sincronização; não são enviados a um modelo generativo de IA. Tokens de sessão são armazenados no armazenamento local do WebView/navegador, como numa aplicação web tradicional; use um dispositivo confiável e mantenha o app atualizado.

## Pesquisa sobre NotebookLM

Estúdio usa regras locais para extrair excertos e construir materiais simples, com referências ao livro e capítulo/trecho. Não substitui o chat generativo fundamentado, o áudio ou outros modelos do NotebookLM. Para trazer um modelo de IA, será necessário um backend de IA com autorização, limites e consentimento explícito para enviar trechos a um provedor de inferência.

## Instalação e migração

O APK usa o identificador `com.lumelib.reader4` e uma assinatura nova, permitindo coexistência com o APK anterior. Exporte o backup ZIP da versão antiga e restaure na nova. O APK foi validado quanto à estrutura e à assinatura v2; falta teste em um dispositivo Android real.

Para o PWA, hospede os arquivos em HTTPS e use a ação de instalação do Chrome. Não execute login/nuvem por `file://` em navegadores restritivos.
