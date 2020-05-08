import com.github.tototoshi.csv._
import scala.collection.mutable.Map
import scala.collection.mutable.ListBuffer

trait StationCollection {
  val station_collection = Map.empty[String, ListBuffer[Seq[String]]]
}

object ReadCSV extends StationCollection {

  def main(args: Array[String]): Unit = {
    val csv_rows = csv_iterator()
    csv_rows foreach assigner
    write_records(station_collection)
    }

  def csv_iterator(): Iterator[Seq[String]] = {
    val reader = CSVReader.open("Divvy_Trips_2019_Q4.csv")
    val csv_rows = reader.iterator
    csv_rows.next() //get past header
    csv_rows
  }

  def assigner(row_list: Seq[String]): Unit = {
    val station_id = row_list(5)
    if (station_collection.contains(station_id)){
      station_collection(station_id) += row_list
    }
    else {
      station_collection += (station_id -> ListBuffer(row_list))
    }
  }

  def write_records(records_collection: Map[String, ListBuffer[Seq[String]]]): Unit = {
    for ((k,v) <- records_collection) {
      val writer = CSVWriter.open(s"$k.csv")
      for (value <- v) writer.writeRow(value)
    }

  }
}
