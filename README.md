If we are using AckMode.MANUAL, which means the offset commit happens later (synchronously at the next poll).

If we want the offset committed immediately when you call ack.acknowledge(), you need:

factory.getContainerProperties().setAckMode(ContainerProperties.AckMode.MANUAL_IMMEDIATE);


MANUAL_IMMEDIATE = commit right away

MANUAL = commit when the poll loop goes back
