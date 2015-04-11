About MogileFS

See http://danga.com/mogilefs/

MogileFS is our open source distributed filesystem. Its properties and features include:

  * Application level -- no special kernel modules required.
  * No single point of failure -- all three components of a MogileFS setup (storage nodes, trackers, and the tracker's database(s)) can be run on multiple machines, so there's no single point of failure. (you can run trackers on the same machines as storage nodes, too, so you don't need 4 machines...) A minimum of 2 machines is recommended.
  * Automatic file replication -- files, based on their "class", are automatically replicated between enough different storage nodes as to satisfy the minimum replica count as requested by their class. For instance, for a photo hosting site you can make original JPEGs have a minimum replica count of 3, but thumbnails and scaled versions only have a replica count of 1 or 2. If you lose the only copy of a thumbnail, the application can just rebuild it. In this way, MogileFS (without RAID) can save money on disks that would otherwise be storing multiple copies of data unnecessarily.
  * "Better than RAID" -- in a non-SAN RAID setup, the disks are redundant, but the host isn't. If you lose the entire machine, the files are inaccessible. MogileFS replicates the files between devices which are on different hosts, so files are always available.
  * Flat Namespace -- Files are identified by named keys in a flat, global namespace. You can create as many namespaces as you'd like, so multiple applications with potentially conflicting keys can run on the same MogileFS installation.
  * Shared-Nothing -- MogileFS doesn't depend on a pricey SAN with shared disks. Every machine maintains its own local disks.
  * No RAID required -- Local disks on MogileFS storage nodes can be in a RAID, or not. It's cheaper not to, as RAID doesn't buy you any safety that MogileFS doesn't already provide.
  * Local filesystem agnostic -- Local disks on MogileFS storage nodes can be formatted with your filesystem of choice (ext3, XFS, etc..). MogileFS does its own internal directory hashing so it doesn't hit filesystem limits such as "max files per directory" or "max directories per directory". Use what you're comfortable with.