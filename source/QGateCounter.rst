.. _QGateCounter:

逻辑门统计
===============

简介
--------------

逻辑门的统计是指统计量子程序、量子线路、量子循环控制或量子条件控制中所有的量子逻辑门（这里也会将测量门统计进去）个数方法。

接口介绍
--------------

我们先用pyqpanda构建一个量子程序：

    .. code-block:: python
          
        prog = QProg()
        prog.insert(X(qubits[0])).insert(Y(qubits[1]))\
            .insert(H(qubits[0])).insert(RX(qubits[0], 3.14))\
            .insert(Measure(qubits[0], cbits[0]))

然后调用接口 ``get_qgate_num`` 统计量子逻辑门的个数，

    .. code-block:: python
          
        number = get_qgate_num(prog)

.. note::  统计 ``QCircuit`` 、 ``QWhileProg`` 、``QIfProg`` 中量子逻辑门的个数和 ``QProg`` 类似。

实例
-------------

    .. code-block:: python
    
        from pyqpanda import *

        if __name__ == "__main__":
            qvm = init_quantum_machine(QMachineType.CPU)
            qubits = qvm.qAlloc_many(2)
            cbits = qvm.cAlloc_many(2)

            prog = QProg()
            
            # 构建量子程序
            prog.insert(X(qubits[0])).insert(Y(qubits[1])).\
                insert(H(qubits[0])).insert(RX(qubits[0], 3.14))\
                .insert(Measure(qubits[0], cbits[0]))

            # 统计逻辑门个数
            number = get_qgate_num(prog)
            print("QGate number: " + str(number))

            qvm.finalize()


运行结果：

    .. code-block:: python

        QGate number: 4

    
.. warning:: 
        新版本中接口名有所调整，旧接口 ``count_gate`` 将由 ``get_qgate_num`` 替代。\
      
        ``count_gate`` 将于下版本去除，请读者知悉。