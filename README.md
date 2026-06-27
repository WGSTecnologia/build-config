# build-config

Build-files **públicos** compartilhados pela frota Java WGS. Contém **apenas** versões e tasks de build — **nenhum segredo**.

## Conteúdo
- `gradle.properties` — versões centralizadas (Spring Boot, Spring Cloud, plugins, libs `*-objects`).
- `tasks/devops.gradle` — task `downloadBuildFiles` (auto-sync, fail-open, sem token).
- `tasks/docker.gradle`, `tasks/copy.gradle` — tasks auxiliares de build.

## Como funciona (auto-sync da frota)
Cada serviço roda `downloadBuildFiles` no build: baixa estes arquivos via `raw.githubusercontent.com` (repo **público**, sem autenticação) e sobrescreve a cópia local versionada. Resultado: atualizar a versão de um framework aqui propaga para toda a frota no próximo build, **sem configurar nada em máquina nenhuma**. Se estiver offline, o build usa a cópia local (fail-open) e segue.

## Atualizar versões
Edite `gradle.properties` (ou as tasks) e faça commit. A frota sincroniza no próximo build.

> Este repo é público **de propósito** — por isso não pode conter segredos. Credenciais de infra ficam no repo privado `dependency-management`.
