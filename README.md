Check Kotlin Dependecies

Projeto Android (Kotlin + Jetpack Compose) para checar e validar dependências Kotlin/AndroidX com um setup moderno de build (Gradle 8.7, AGP 8.5.2,
Kotlin 2.0.0, JUnit 5).

<!-- https://github.com/fernandorubini/CheckKotlinDependecies -->

Objetivo

Servir como template/base de referência para iniciar projetos Android com Compose e inspecionar a compatibilidade de dependências,
evitando atritos iniciais de configuração (AndroidX, Kotlin/Compose, Gradle/AGP, testes com JUnit 5 etc.).

Stack e versões

Gradle Wrapper: 8.7
Android Gradle Plugin (AGP): 8.5.2
Kotlin: 2.0.0
Jetpack Compose: via Compose BOM 2024.06.00
compileSdk / targetSdk: 36
minSdk: 24
JUnit 5 (Jupiter) para testes unitários com useJUnitPlatform()


Pré-requisitos

JDK 17
Android Studio (versão recente compatível com AGP 8.5+)
Gradle Wrapper


Como rodar

Build (Debug)
./gradlew clean assembleDebug


Executar testes unitários (JUnit 5)

./gradlew testDebugUnitTest

(Opcional) Instalar no dispositivo/emulador
./gradlew installDebug


Teste exemplo (JUnit 5)

app/src/test/java/com/fernandodev/checkkotlindependecies/ExampleJUnit5Test.kt

package com.fernandodev.checkkotlindependecies

import org.junit.jupiter.api.Assertions.assertEquals
import org.junit.jupiter.api.Test

class ExampleJUnit5Test {

    @Test
    fun `2 + 2 deve ser 4`() {
        assertEquals(4, 2 + 2)
    }
}


Rode com:

./gradlew testDebugUnitTest

O projeto já está configurado com useJUnitPlatform() (Android DSL), garantindo a execução no JUnit 5.


Estrutura do projeto

CheckKotlinDependecies-master
├── .gitignore
├── .idea/
├── README.md
├── build.gradle.kts
├── gradle/
│   ├── libs.versions.toml
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle.kts
└── app/
├── build.gradle.kts
└── src/
└── main/
└── kotlin/
└── Main.kt


Catálogo de dependências (Version Catalog)

As versões principais (AGP, Kotlin, Compose BOM, AndroidX) estão definidas em gradle/libs.versions.toml. No app/build.gradle.kts, as libs são referenciadas como libs.androidx.core.ktx, 
platform(libs.androidx.compose.bom), libs.androidx.material3, etc.


Benefícios:

Centraliza versões;
Facilita upgrades;
Mantém coerência entre módulos.


⚙️ Configurações principais

gradle/wrapper/gradle-wrapper.properties
distributionUrl=https\://services.gradle.org/distributions/gradle-8.7-all.zip
gradle.properties
android.useAndroidX=true
android.enableJetifier=true
org.gradle.jvmargs=-Xmx4096m -Dfile.encoding=UTF-8 -XX:+UseParallelGC -XX:MaxMetaspaceSize=1g
org.gradle.daemon=true
org.gradle.parallel=true
org.gradle.configureondemand=true
org.gradle.caching=true
kotlin.code.style=official
kotlin.incremental=true
kotlin.daemon.jvmargs=-Xmx2048m


Trecho relevante no app/build.gradle.kts
android {
// ...
testOptions {
unitTests.all {
// Em Android, chame via 'it.' se necessário:
it.useJUnitPlatform()
}
}
}


CI (GitHub Actions)

Workflow em .github/workflows/android-ci.yml


Versões/compatibilidade (Gradle/AGP/Kotlin):
Gradle 8.7 + AGP 8.5.2 + Kotlin 2.0.0.


Roadmap

Adicionar exemplos de instrumented tests (androidTest/)
Adicionar lint/Detekt e task de verificação no CI
Publicar sample do app (telas Compose)
Escrever guia de upgrade (AGP/Kotlin/Compose)


Tópicos

android · kotlin · jetpack-compose · gradle · androidx · junit5 · template · ci-cd

[![CI](https://github.com/fernandorubini/CheckKotlinDependecies/actions/workflows/android-ci.yml/badge.svg)](https://github.com/fernandorubini/CheckKotlinDependecies/actions/workflows/android-ci.yml)



Autor

Fernando Rubini
https://github.com/fernandorubini
www.linkedin.com/in/fernando-rubini-dev-549abb24


[![CI](https://github.com/fernandorubini/CheckKotlinDependecies/actions/workflows/android-ci.yml/badge.svg)](https://github.com/fernandorubini/CheckKotlinDependecies/actions/workflows/android-ci.yml)
