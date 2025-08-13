@Bean
public DefaultErrorHandler kafkaErrorHandler() {
    DefaultErrorHandler errorHandler = new DefaultErrorHandler((record, ex) -> {
        log.error("Kafka ErrorHandler caught exception for record: {}, Error: {}", record, ex.getMessage(), ex);
      
    });
  
    return errorHandler;
}

@Bean
public KafkaListenerContainerFactory<?> kafkaListenerContainerFactory() {
    ConcurrentKafkaListenerContainerFactory<Object, Object> factory = new ConcurrentKafkaListenerContainerFactory<>();
    factory.setConsumerFactory(consumerFactory());
    factory.setCommonErrorHandler(kafkaErrorHandler());
    return factory;
}
