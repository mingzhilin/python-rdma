InfiniBand Architecture (IBA) Definitions
=========================================

The majority of these definitions apply only to InfiniBand and are not
applicable to general RDMA devices. However, a few are used as part of the
kernel API for all device types (eg :data:`~rdma.IBA.NODE_CA`).

For ease of use it is recommended to import this module as::

    import rdma.IBA as IBA;

The module includes Python versions of the IBA defined binary structure. The
Python version is unpacked, accessing the IBA defined member names is simply
done by acessing the property name. The tables in the reference indicate
the valid member names, the bit position ``start_bit:end_bit (bit count)``
and a description of the Python type used for the attribute.

The class attributes starting with ``MAD_`` are metadata used by the RPC
functions in :class:`rdma.madtransactor.MADTransactor` to generate the correct
attribute ID, and validate that the RPC is valid.

All classes in this section are derived from :class:`rdma.binstruct.BinStruct`
and contain implementations of those methods. Use the
:meth:`~rdma.binstruct.BinStruct.pack_into` and
:meth:`~rdma.binstruct.BinStruct.unpack_from` methods to produce the
binary layout of the structure.

Constructors will also accept a bytes or another
:class:`~rdma.binstruct.BinStruct` instance::

   data = bytes('\0'*IBA.SMPFormat.MAD_LENGTH);
   hdr = IBA.MADHeader(data);
   sfmt = IBA.SMPFormat(hdr);
   dfmt = IBA.SMPFormatDirected(sfmt);

When referring to another :class:`~rdma.binstruct.BinStruct` instance the
new instance is unpacked using the original byte buffer that the first instance
was unpacked from. Changing the attributes has no effect.

.. NOTE::
   This is based on Pythons :mod:`struct` module, which requires a :class:`bytes`
   object for unpack and a :class:`bytearray` for packing.

Structures named ``*Format`` are generally a full MAD, and need to be 'casted'
to read the data::

   fmt = IBA.SMPFormat(data);
   pinf = IBA.SMPPortInfo(fmt.data);

:mod:`rdma.binstruct` IBA Structure Helpers
-------------------------------------------
.. automodule:: rdma.binstruct
   :members:
   :undoc-members:

:mod:`rdma.IBA` InfiniBand Architecture (IBA) definitions
---------------------------------------------------------
.. automodule:: rdma.IBA
   :members: GID,GUID,mad_status_to_str
   :undoc-members:
   :show-inheritance:

.. module_data:: rdma.IBA

:mod:`rmda.IBA` Binary Structures
---------------------------------

.. include:: iba_struct.inc