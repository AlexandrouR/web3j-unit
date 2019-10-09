**⚠️ This is a work in progress! ⚠**

### Getting Started

1. Add dependency to gradle.

```groovy
   repositories {
      maven { url 'https://oss.sonatype.org/content/repositories/snapshots' }
        maven { url "https://dl.bintray.com/ethereum/maven" }
   }

   testImplementation "org.web3j:web3j-unit:4.6.0-SNAPSHOT"
```
or if JUnit already exists as a dependency:
```
testImplementation ("org.web3j:web3j-unit:4.6.0-SNAPSHOT"){
      exclude group:'org.junit.jupiter'
    }
```

2. Create a new test with the `@EVMTest` annotation.

```java
@EVMTest
class GreeterTest {

}
```

3. Inject instance of `Web3j` `TransactionManager` and `ContractGasProvider` in your test method.

```java
@EVMTest
class GreeterTest {

@Test
    fun greeterDeploys(
        web3j: Web3j,
        transactionManager: TransactionManager,
        gasProvider: ContractGasProvider
    ) {}
}
```

4. Deploy your contract in the test.

```java
@EVMTest
class GreeterTest {

    @Test
    fun greeterDeploys(
        web3j: Web3j,
        transactionManager: TransactionManager,
        gasProvider: ContractGasProvider
    ) {
        val greeter = Greeter.deploy(web3j, transactionManager, gasProvider, "Hello EVM").send()
        val greeting = greeter.greet().send()
        assertEquals("Hello EVM", greeting)
    }
}
```

5. Run the test!
