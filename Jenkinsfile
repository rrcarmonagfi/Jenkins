RESULTADO = "RESULTADO\n"
pipeline
{
    agent any
    
    environment
    {
      MI_NUMERO_1 = 40
      MI_NUMERO_2 = 20
      
    }
    
    options
    {
        timeout(time: 5, unit:"MINUTES") //Timeout
        //errorHandling() //Manejo de errores
        skipStagesAfterUnstable() // Se saltea todo lo que venga a posterior si la ejecución es INESTABLE. 
    }
    
    stages
    {
        stage ("Operaciones aritméticas")
        {
            steps
            {
                script
                {
                  suma = env.MI_NUMERO_1.toInteger() + env.MI_NUMERO_2.toInteger()
                  resta = env.MI_NUMERO_1.toInteger() - env.MI_NUMERO_2.toInteger()
                  multiplicacion = env.MI_NUMERO_1.toInteger() * env.MI_NUMERO_2.toInteger()
                  division = env.MI_NUMERO_1.toInteger() / env.MI_NUMERO_2.toInteger()
                  RESULTADO = 
                    "${MI_NUMERO_1} + ${MI_NUMERO_2}" + ' = ' + suma + '\n' +
                    "${MI_NUMERO_1} - ${MI_NUMERO_2}" + ' = ' + resta + '\n' +
                    "${MI_NUMERO_1} * ${MI_NUMERO_2}" + ' = ' + multiplicacion + '\n' +
                    "${MI_NUMERO_1} / ${MI_NUMERO_2}" + ' = ' + division
                println RESULTADO
                }
            }
        }
        stage ("Comandos")
        {
            steps
            {
                script
                {
                  bat "ipconfig /flushdns"
                }
            }
        }
        stage ("Generar fichero STAGE1")
        {
            steps
            {
                script
                {
                    println "El resultado es " + RESULTADO
                  writeFile(file: "C:\\Users\\rafael.rodriguez\\Documents\\CURSO_JENKINS\\pipelineEjercicio3.txt", text: RESULTADO)
                }
            }
        }
    }
    post
    {
        always 
        {
            echo "El pipeline se ejecutó."
        }
        failure 
        {
            echo "El pipeline falló"
            mail to: "soporte@dominio.com", subject: "Pipeline Falló", body: "El pipeline no se ejecutó correctamente."        
        }
        unstable
        {
            echo "El pipeline no se ejecuto de forma estable."
        }
        success
        {
            echo "Fichero generado!!"        
        }
    }
}
