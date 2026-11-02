# GxOS

GxOS é uma imagem Live Linux personalizada baseada em Debian, com ambiente gráfico XFCE.

## Construir sem WSL e sem VM local

O GitHub Actions constrói a imagem num runner Linux hospedado pelo GitHub. No teu PC Windows precisas apenas de um navegador para configurar o repositório e descarregar o artefacto. O QEMU pode ser usado depois para testar o ISO.

## Ficheiros incluídos

- `.github/workflows/build-iso.yml` — workflow de construção.
- `config/package-lists/gxos.list.chroot` — pacotes incluídos.
- `config/includes.chroot/etc/issue` — mensagem apresentada nos terminais.
- `config/includes.chroot/etc/motd` — mensagem de boas-vindas.

## Como usar

1. Cria um repositório no GitHub chamado `GxOS`.
2. Carrega todos os ficheiros desta pasta para a raiz do repositório, preservando as pastas.
3. Abre o separador **Actions** do repositório.
4. Escolhe **Build GxOS ISO** e clica em **Run workflow**. Também podes fazer push para `main` quando alterares os ficheiros `config/**`.
5. Aguarda a conclusão do workflow.
6. Abre a execução concluída e, na secção **Artifacts**, descarrega `GxOS-ISO-amd64`.
7. Extrai o ZIP do artefacto. Deverás encontrar `GxOS-amd64.iso` e `GxOS-amd64.iso.sha256`.

## Notas

- A primeira construção pode demorar vários minutos e pode falhar se o runner, um espelho Debian ou uma dependência estiver temporariamente indisponível.
- O workflow usa `live-build` do runner Ubuntu para gerar uma imagem Live baseada em Debian stable; não instala o sistema no disco do PC.
- A imagem inicial usa o desktop XFCE e Firefox ESR. A marca GxOS está presente nas mensagens de terminal, mas o tema gráfico, o ecrã de arranque e o instalador ainda não estão personalizados.
- O artefacto é guardado durante 14 dias. Volta a executar o workflow para gerar outro.
- O workflow usa ações oficiais de checkout e upload-artifact com tags principais. Para ambientes de produção, considera fixar as ações por SHA completo.
- Não uses a ISO numa máquina real antes de a testar num ambiente isolado.
